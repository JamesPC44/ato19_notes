## Link

https://allthingsopen.org/talk/test-automation-without-assertions/

## Notes

- Just because the test passes doesn't mean it tested what you wanted
  (umbrella open != umbrella working)
- Does not test what the user cares about
  - Missing CSS will not show up
  - Tests have to care about ids
- Solution
  - don't define the test, approve it
- Manual tests find bugs
- automated tests are always regression tests
- _the code is not the software_ (the experience the user has)

### Solution

- Golden Master testing - (question: how do you get it in that working initial state?)
- Challenges
  1. Noise
  2. Redundancy

### Noise

- deny list of changes
- analogy with version control: gitignore
check everything <--> check nothing

- At Google, have unicorns for new features so QA knows it's new
  - eventually got pushed to production by accident
- If you don't expect it, you can't guard against it
- Want a whitelist, not a blacklist
  - Compare firewalls

### Solution

- recheck.ignore
  - matcher: id=div-b4dfad, attribute-regex: font.\*
  - matcher: xpath=html[1]/body[1]/div[1]/div[1]/div[1]
- basically a filter
- everything else is tracked

The rest of this talk is a demo of the rechecker project.

## References

- https://en.wikipedia.org/wiki/Characterization_test
- https://retest.de
