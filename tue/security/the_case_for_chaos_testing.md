# ATO19: The Case for Chaos Testing

*Peter Lamar*

https://allthingsopen.org/talk/the-case-for-chaos-testing/

## Complexity
- It's easy to build software that becomes complex.
- Fight complexity, one line at a time.
- Even in the best systems, complexity grows over time.
- [graphs and diagrams, "Death Star diagrams"]
- As you add features and value, complexity grows.
- Controlled experiments would be nice if they could identify weaknesses in the system.

## Chaos Engineering
- Cool name for the controlled experiments.
- Like a vaccine; inject a small amount of virus to build immunity.
> "You have to build up to the crazy 'Let's drop half our cluster and see what happens!'"
- Principlesofchaos.org

## Expected Benefits
- Less downtime, better user experience.
- Less alarms and alerts (and burnout!) to Ops/SRE/Dev teams.
- More productivity from fewer unplanned outages.
- Spreading knowledge of application to team (less firefighting, so you have time to mentor).

## Steps
1. Define normal/steady state of the system.
2. Pseudo-randomly inject faults, and see if behavior adapts correctly.

## Experiment Design
Speaker had a table with these columns:
- Failure scenario
- Experiment
- Scoping
- Signals metrics
- Abort conditions
- Expected outcomes
- Actual outcomes
- Found bugs

## Tools
- Chaos toolkit
- Chaos blade
- Chaoskube 
- Gremlin
- Litmus
- Powerful seal

## Live Demo
- Pumba (tests latency)
- Speaker knew how to crank out some fierce Docker commands, or had printed notes.
- Chaos Blade (more network delays)
	- May be able to directly inject exceptions into the JVM.
- Speaker notes that automating chaos experiments is very worthwhile.
- Litmus (Kubernetes chaos testing)
- Anti-pattern: Having to edit a really long script to make Jenkins go and do the testing.

## Review
1. Have a hypothesis.
2. Use real-world events and limited scope.
3. Make it as real as possible, ideally production.
4. Collect results at the end, drive future experiments? (Didn't get the last one copied down, so I'm guessing.)

Design points:
6. Minimize the blast radius.
7. Have an emergency stop button.

## Questions
> "What's the most interesting bug you've found with chaos testing?"
- Answer: Security issues, developer mistakes. (Example given was discovering an old version of a company app had basically no authentication.)
