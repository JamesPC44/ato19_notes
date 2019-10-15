## Link

https://allthingsopen.org/talk/the-case-for-chaos-testing/

## Notes

### Complexity

- Easy to build complex software
- Fight complexity one line at a time
- Features bring complexity
- Would be nice to identify weaknesses in system

### Failure

- companies are failing all the time
  - amazon, google, ...
- chaos testing: controlled experiments to see how apps behave in production
- like a vaccine: build immunity
- Normally, play levels at random - if you play last level you get destroyed
  - can build up to the 'full crazy drop half our cluster and see what happens'

### Chaos Engineering

- Benefits
  - Less downtime, better UI
  - fewer alarms, unplanned outages
- Method
  - Observe normal application state
    - logs
    - traffic
    - what's the best indicator you're acting healthy?
  - Create hypothesis
  - Inject faults
    - Crash containers
    - Kill network
    - See differences between control and experiment groups

- Example: Latency

### Tools

Sponsored by CNCF

- ChaosToolkit
- ChaosBlade
- ChaosKube
- Gremlin
- Litmus
- 

### Live Demos

#### Pumba

- tests latency
- Baseline: 12 ms
- With Pumba: 4200ms

#### Blade

- can inject exceptions into JVM
- simulates application response to a server 500
- avoids cascading failure
- Base: can curl a website

### Summary

- Want to run as close to production as possible
- Tests:
  - stack component
  - availability zones
  - slowdown services (esp. database)

## Questions

- ???
  - Easier to manipulate files checked into git than Jenkins
- What's the worst bug you found?
  - Things that were so bad we didn't want to tell the business
  - Security issues
  - Source code sitting open to the public
  - Terrifying

## Resources

- https://principlesofchaos.org/?lang=ENcontent
- https://github.com/alexei-led/pumba
- https://www.cncf.io/
- https://github.com/peterlamar/the-case-for-chaos-testing
- https://github.com/chaosblade-io/chaosblade
- https://docs.litmuschaos.io/docs/getstarted/
