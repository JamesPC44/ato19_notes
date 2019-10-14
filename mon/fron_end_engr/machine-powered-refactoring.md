# Machine Powered Refactoring

## Link

https://allthingsopen.org/talk/machine-powered-refactoring-leverage-asts-to-push-your-legacy-code-the-web-forward/

## Notes

- ASTs are stuck in library-author-land

- are you happy with your app?
  - Yes? Is it hello-world?
  - Greenfield :P
- real products have cruft
  - multiple frameworks, too many dependencies, etc.
  - once we normalize that, we can address it
- most web traffic is mobile
- tons of javascript
  - median is 400 KB, up to 15 seconds until interactive
  - big problems
- view-source is kind of useless:
  - transpilers
  - bundlers

- can use ASTs to programmatically explore code
  - linters
  - reflection

*brief overview of how compilers work*
- [v8 pic]

### Issues

- More code

### What can ASTs do?

- Automate code transformation
- Used for Angular, babel, jshint/eslint, etc.

### How to improve code

- Lint?
  - No? Unit test?
  - No? Integration test

### Back to JS

- node_modules are :(
- 1:10 user:library coverage (speaker: 'and that's a good thing!' :X)
- bad habit of rewriting code-bases
- most transformers are taking ES6 -> backwards compatible
- linters are taking cruft -> ES6
- `preval` -> metaprogramming in Babel 🙃
- trying to do this with regex is doomed to failure

## Questions

- Have you thought about automatically updating dependencies with ASTs?
  - Would be really cool, didn't have time in the talk

## Resources

- https://astexplorer.net/
- [v8 pic](https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775)
- https://github.com/facebook/jscodeshift

## Meta

- Speaker trying to do audience interaction but looking for very specific answers
- Wish they talked about how it's generally applicable rather than 'how to do cool things with Babel'
