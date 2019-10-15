# ATO19: Getting Started with Flatpak

*Rosemary Wang*

https://allthingsopen.org/talk/everything-as-code-with-terraform/

## Infra-as-code
 - Unify view of resources.
 - Tech agnostic.
 - Manage everything with an API.

## Terraform
 - Hashicorp config language.
 - Can create/destroy/update/delete.
 - Controlled by **Providers**.

## Providers
### Terraform Core
 - gRPC client
 - Config language
 - State management
 - Resource graph
 - Plan execution

### Plugins
 - gRPC servers (essentially binaries pulled down from a central package repo)
 - Exec API calls against target API

## Live Demo
 - Speaker moved to a TDD-based Go demo. Skipped over a bunch of stuff.

## Resources
 - https://github.com/joatman08/2019-demo-ato

## Tips
 - Non-ideal APIs exist upstream sometimes.
     - Some are read-only.
     - Sometimes you have to provide your own client.
 - Make acceptance tests for your providers.
