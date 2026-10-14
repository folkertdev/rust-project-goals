# Simplify the simpleinfra IaC setup

| Metadata              |                             |
| :-------------------- | --------------------------- |
| Contact               | @marcoieni                  |
| Status                | Proposed                    |
| Other tracking issues | [rust-lang/simpleinfra#962] |
| Zulip channel         | [#t-infra]                  |

## Summary

Simplify the Infrastructure as Code (IaC) setup in [simpleinfra] by using a single tool instead of both [Terraform] and [Terragrunt].
The new setup should make deployments easier to automate in the future, so that they can eventually run from a secure, centralized environment instead of the laptops of [infra admins].

## Motivation

### The status quo

Our IaC setup currently uses both Terraform and Terragrunt. As described in [rust-lang/simpleinfra#962], the unfinished Terragrunt migration has left us with:

- different deployment workflows (related to Terraform or Terragrunt) depending on the project, which adds cognitive load and makes scripting deployments harder.
- duplicated modules (e.g. `bastion` and `ecs-task`) that need to be maintained in both setups.

Today, infra admins deploy infrastructure from their own laptops. These machines also run everyday development tools and third-party software, so a malware could put infrastructure access at risk.

### What we propose to do about it

We will investigate whether using both Terraform and Terragrunt is still worthwhile. We will review why Terragrunt was introduced, what capabilities we need today, and whether Terraform (or an alternative such as OpenTofu) now covers them. The evaluation will explicitly consider how easy each option is to automate.

We will then agree on an approach with the infra team and migrate the codebase to it.

Once the IaC setup is simplified, we want to automate deployments and run them from a secure, centralized environment but this is out of scope for this goal.

### Work items over the next year

| Task                                        | Owner(s)                     | Notes                                                                                                    |
| ------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------- |
| Evaluate the Terraform and Terragrunt setup | @marcoieni, @ubiratansoares  | Investigate the requirements and tradeoffs in [rust-lang/simpleinfra#962], including ease of automation. |
| Agree on the approach with the infra team   | @marcoieni, @ubiratansoares  |                                                                                                          |
| Migrate to the simplified IaC setup         | @marcoieni, @ubiratansoares  |                                                                                                          |

## Team asks

| Team    | Support level | Notes                                                                 |
| ------- | ------------- | --------------------------------------------------- |
| [infra] | Small         | Review and approve the IaC simplification approach. |

## Frequently asked questions

### Why not automate deployments as part of this goal, too?

We want to keep this goal small and achievable. Simplifying the setup first lets us automate later with less effort.

[simpleinfra]: https://github.com/rust-lang/simpleinfra
[#t-infra]: https://rust-lang.zulipchat.com/#narrow/channel/242791-t-infra
[infra admins]: https://github.com/rust-lang/team/blob/main/teams/infra-admins.toml
[Terraform]: https://developer.hashicorp.com/terraform
[Terragrunt]: https://terragrunt.com/
