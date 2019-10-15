# ATO19: Getting Started with Flatpak

*Klaatu Einzelganger*

https://allthingsopen.org/talk/getting-started-with-flatpak/

## Old world
- Disc had applications onboard with the distribution.
- Repo considered part of the OS.

## Limitations of old world
- Proprietary apps.
- Newbie devs porting stuff over to Linux for the first time.
- Too many packaging formats!
- Reality is that volunteers can't pull in every new application out there into the repo systems.

## Flatpak
- Centralized or decentralized distribution.
- Devs submit manifest + package to App Store, allowing direct-to-user distribution.
- Builds on container tech, condoning applications off from the rest of the world. (Good for outdated dependencies. Old hat feature on Mac OSX.)

## Flatpak inefficiencies
- Bloated package sizes (mitigated somewhat by SDKs/predefined components)

## Building Flatpaks
- Live demo of packaging a hello world.
- `sudo apt install flatpak`
- Install Flatpak itself, the builder, and tools.
- Write JSON or YAML manifest file. (Ex: `org.gnu.Hello.yaml`, where name of app is capitalized.)
	- `app-id`
	- `runtime`
	- `runtime-version`
	- `sdk`
	- `command` (optional in some cases)
	- Modules
		- `name`
		- `buildsystem` (Speaker thinks auto tools is fine. Bleh)
		- `no-autogen`
		- Sources
			- `type: archive`
			- `path: src/hello-...`
			- (Optional) `url: ...`
- Speaker copies in code from something he'd hacked up earlier
- Flatpak-builder used to auto config and build everything
- Can use the builder tool to run the Flatpak as well

## Audience Question
> "Can we cache build products and dependencies?"
- Answer: Yes, local repos are possible. Thumb drives, web servers, etc.

## GUIs with Flatpak
> "I generally don't get excited about technology until I can play Tetris on my system."
- Kblocks example.
- Much more complex manifest, has several sub modules.
- Permissions can be set for apps inside the Flatpak containers.
- User icons can be set, and everything works, while shielded from the rest of the system.

## Building a repo
- Uses the Flatpak builder.
- Can turn a local folder into a repo.
- Can sign repositories!
- Flathub serves as a centralized repo if you don't want to host your own.
- Many manifest examples exist.

## Audience Questions
> "What's new? What features are upcoming?"
- Answer: Better CLI experience
- Speaker notes that the future may be flatpaks and containers running around a small core OS that doesn't change much.

