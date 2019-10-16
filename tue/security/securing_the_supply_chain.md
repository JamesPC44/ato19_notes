# ATO19:  Securing the Supply Chain

*Wes Widner*

https://allthingsopen.org/talk/securing-the-development-supply-chain/

## Setting the scene
> "When I was looking at the nightly builds...that's not how we did it in the DoD." (Senator quote)

## Developing a security mindset
- Devs have incredible access to critical systems.
	- Naturally makes them targets
	- Makes them insider threats
- Appropriate paranoia, not unfathomable paranoia
- Means we need to scale our distress by the **probability** and **severity** of risk.
- Helps us scope our efforts and make meaningful progress in securing our systems.

## Foxconn hack
- Likely a hoax.
- "Having a well done nation-level hardware implant surface, is like watching a unicorn jump over a fence" (outside quote)
- Likely inspired by the NSA intercept facility stories.

## Facebook and Apple hacks
- Watering hole attack on the devs at FB and Apple.

## Owning the problem
- Not just appsec's job.
- A good organization will have a dedicated application security team.
- This doesn't absolve devs of being good citizens.
- Castle security is dead, stop expecting someone else to defend your fort.
- Every engineer needs to be doing their part in the organization's defense. (Layered defense)

## Sony hack
- Piggybacked off a phishing attack. (Spearphishing)


## Choose your libraries wisely
- Questions to ask:
	- Is this library absolutely necessary?
	- Has another team already chosen a similar library?
	- How healthy is this library?
	- Are you willing to care for and feed it?
	- How could it break?
	- What would it impact?
	- How would I know?
- Do:
	- Proactively vendor everything.
	- Don't automatically pull from external sources.

## Leftpad debacle and Formjacking

## Beware of entangling alliances
(Quoted from George Washington)

## Keep your friends close
- 3rd party apps make our lives easier, but it comes with a cost. (CircleCI, and friends, etc.)
- Each integration adds systemic risk.
- Be mindful of what you're purchasing for all that risk.
- Be proactive in securing those integrations.


## Dockerhub hack

## GitHub password exposure
- "Everything you own has a claim on you."
	- It claims part of your attention, your time, and so on.
	- The clutter in your home occupies space in your mind too. (Applies to codebases as much as real life.)
- What you own requires care and feeding. Otherwise, it becomes a liability.

## Be the change you wish to see
- As engineers, we can and should set the example for others to follow.
- Use password managers, Secure Enclave's, 2FA, etc.
- Don't hardcore credentials into scripts, and certainly don't check those into source control.
- Embrace security controls, don't fight them.

## Don't take shortcuts!
- Once committed, it could be cached by another system.
- Sooooo many Github commits of "remove password", and so on.
- If it got out there, it's compromised.

## Loose lips sink ships!
- ASUS engineers had passwords checked into Github for months.

## Use your influence wisely
- We should use our influence over the systems we engineer to make doing the right things (secure things) easy.
- Be the one in the meeting who asks the hard questions about security.
- "Would our press release on a breach be able to show that a user went dramatically out of their way to be insecure?"

## Recognize the attack surface
- It's broader than you think.
- Don't accept lame answers like: "this will never be exposed to the internet."
	- This has been the primary source of many breaches.
	- Implicitly assumes a castle mindset.
- Assume your environment is already breached, and align accordingly.
- Don't wait for an incident to come up with contingency plans.

## Tesla's cloud was used to mine cryptocurrency
- "Cryptojacking attack"

## Be a security bar-raiser
- Stand up for ProdSec when they try to level up your security posture. (Don't fight them! Ask them how they'd do it while achieving the same goals you have.)
- Come up with fun ways to enable and encourage everyone to be more secure.
- Every little bit you do raises the cost to an attacker.

## "Only you can prevent lateral movement" meme (Smokey the Bear)

