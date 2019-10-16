# ATO19: Hidden Dragons of CGO

*K. S. Bhaksar*

https://allthingsopen.org/talk/hidden-dragons-of-cgo/

## Quotes during the talk
> "C is a good assembly language."

> I used to be a programmer, but when I couldnt do useful work anymore, they made me a manager!"

> Most programmers have 1 error per 1000 lines of code ... I have 2 errors per line!"

## YottaDB
- High performance KV store.
- Written in C.
- Provides a detailed C API.

## Go API for YottaDB
- Provides a similar API to the C version.
- They wrote the docs first, then the code for the API.
- They thought it would be simple.
- (Picture shown of a dragon eating a man's head)

## CGO
- Allows Go to access C libraries.
- Key takeaways: Go pointers have special restrictions. Those restrictions are detailed, and the docs around them are long, and very dry.

## C strings != Go Strings
- Have to pass an array of bytes to C and give C the address of the first element.
- `Unsafe.Pointer` protects the string from the Go garbage collector.

## Cannot pass Go structs with pointers to C structs
- `defer` required to schedule deallocation of C structs.
    - This is error-prone, and results in memory leaks when you make mistakes.
- Other approach is to use Finalizers.
    - This approach annoys Gophers.
    - `KeepAlive` provides a "last living reference" to an object, so that it won't get GC'd.

## Callbacks
- YottaDB uses callbacks for ACID transactions.
- "Obvious" way (2x definitions) has issues:
    - Kludgy.
    - Difficult to test.

## Alternatives approach to Callbacks
- Hashmap index + closure for parameter passing.
> "Keep the Gophers happy!"

## Taming the CGO dragon
- Keep poking the dragon.
- `export CGOC=1` :: More GC happens.
- `cgocheck=2` :: Catch Go pointers being passed across the boundary.
- Horrible. Mean. Ugly. Tests.

> "One of the reasons I have so little hair \[is the random CGO failures\]."

## Dragons slumbering, not slain
- Go believes it owns the whole process.
- Signal handlers -- another dragon.
- *The cost of sharing a cave with a dragon is eternal vigilance.*
    - Test continuously, then test some more.

## Dragon sleighing
- Picture of dragons hitched up to sleighs.

## Questions
> "How was your experience contacting the Golang team?
- Answer: The golangnuts chat.
  Had to do a lot of filtering the wheat from the chaff in responses though.
  Many, many unhelpful or rude responses.

> "Is the DB in the same process as the program using it?"
- Answer: Yes, it's in the process's address space.

> "May we have a copy of these slides?"
- Answer: Email me.

