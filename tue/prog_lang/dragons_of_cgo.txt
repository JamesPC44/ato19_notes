## Link

https://allthingsopen.org/talk/hidden-dragons-of-cgo/

## Notes

- 'Go is fine - the problem happens when you step outside for a bit'

### About YottaDB

- Key-Value tuples
- Everything sorted
- Schemaless - can mix key sizes and key types

### C

- Can talk to any language
- YottaDB has C API

### Go

- Static typing
- Cooperative multithreadin
- Mix of C, Erlang, and Java

### Implementing Yotta

- Wrote docs for API first
- API basically same as C but thread-safe
- Funding through support contracts and funded enhancements
- C wrapper for Go API seems simple, took more effort than anticipated

### CGO

- C is not garbage collected, need to malloc/free
- CGO creates rules for memory
- go strings are not C strings: need to cast to ([]byte) and pass address of first element
- Cannot pass a pointer to a struct
- Can use unsafe casts, but then it just panics at runtime
- Can cast to CString: `C.mystruct{C.CString("world")}`
  - but leaks memory, because go assumes that calling function frees memory
- Solution: `defer C.free(msg.msg)`
  - compiles, runs, and works, but error-prone, need manual memory management again
- `SetFinalizer` can do this automatically - but the pointer passed to the C function can get garbage collected!
  - Solution: `runtime.KeepAlive(msg)`

### Callbacks

- Used for transaction processing
- 'Optimistic concurrency control'
  - Create a function
  - function calls database
  - if it cannot commit, restart the transaction
  - not common, but scales well
- Problem occurs when an external function needs to call back into go
- Need to make 2 separate files: one which calls Go -> C, other C -> Go
- Drawbacks
  - Error prone: defined in two places
  - Hard to test, can't import C in test code
- Alternate approach

### CGO Dragons
- Nondeterministic
- May garbage collect while you're calling a function
- Catch pointers being passed: `GODEBUG='cgocheck=2'`
- Garbage collect more: `GOGC=1`
- Very ugly tests
- Expected to be 3 months, was 1 year
- Slumbering, not slain
  - Go believes it owns the process
  - Cost of sharing a cave with a dragon is eternal vigilance
- Haven't even discussed signal handlers

- Database runs _inside_ of process, not in client/server
  - TCP connection available, but no transactions available

## Resources

- https://golang.org/cmd/cgo/

## Meta

- Would love to work at this company
