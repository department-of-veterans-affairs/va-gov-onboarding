---
permalink: /platform-overview/support
---

# Support

## Support Slack Channel

If you need assistance from someone on the Platform, see [Getting help from the Platform in Slack](https://depo-platform-documentation.scrollhelp.site/support/getting-help-from-the-platform-in-slack).

> **Note:** Avoid direct messaging a Platform team member. Chatting openly in the #vfs-platform-support channel allows others to learn from the questions and answers discussed.

## Support Request Policies

1. **Support request response time:** 3 business hours (8:00 a.m. - 6:00 p.m. ET, Monday through Friday).

- We'll acknowledge that we received your support request within 3 business hours. The time it takes us to resolve your issue will depend on the complexity of the issue.

2. **Support request scope:** 30 minutes or less

- To ensure that everyone has access to responsive support, requests exceeding 30 minutes of support engineer time will be escalated to a critical incident (see “Is my issue critical” below) or a feature request. To request priority escalation, you should communicate with your team’s OCTO-DE lead.

3. **Pull request review response time:** 1 business day

- Sometimes you may need a pull request review completed in less than 1 business day. We’ll do our best to accommodate urgent requests. To request an urgent PR review, post in the #vfs-platform-support Slack channel. Be sure to explain:
  - Why the PR review request is urgent
  - When you would like the PR reviewed by
- The on-call support engineer will evaluate your request and let you know whether or not your PR can be reviewed by your desired deadline.
  > **Note:** You only need to ask about a PR review in #vfs-platform-support if the PR review takes longer than 1 business day or if you need to request an urgent review.

## Platform engineering reviews

To help ensure that we maintain consistent code quality and performance for the best user experience across VA.gov, we require that you have your work reviewed at certain points throughout your development cycle.

## Pull request code reviews

After your code is reviewed by another member of your team and before it's merged, your code must be reviewed by a Platform engineer.

For more information on code reviews, see [Submitting pull requests for approval](https://depo-platform-documentation.scrollhelp.site/developer-docs/submitting-pull-requests-for-approval).

## Security and privacy review

This review happens before you begin rolling out your new feature to ensure your feature meets DEPO platform privacy and security standards.

For information on requesting a security and privacy review meeting, see [Privacy, security, infrastructure readiness review](https://depo-platform-documentation.scrollhelp.site/collaboration-cycle/privacy-security-infrastructure-readiness-review).

## Resolve critical issues on the trunk branch

We always intend to keep our repositories deployable from trunk branches. VA.gov doesn't use release branches. We focus on keeping the trunk branches healthy. This means that problematic code in trunk branches should be resolved as quickly as possible.

### Is my issue critical?

Examples of critical issues include:

- A bug that’s preventing a significant number of Veterans from accessing a feature
- A bug creating a non-trivial deviation from expected functionality
- A 508/accessibility failure of severity level 0 (Showstopper) or 1 (Critical) (severity rubric)

Examples of non-critical issues include:

- Incorrect text or visual formatting that does not impede the feature from working
- Any code for features not yet released to Veterans
- Just wanting to get code out sooner

When in doubt on whether an issue is critical enough for out-of-band deployment, OCTO-DE leadership for the Platform will decide.

### Fix forward or revert?

When an issue in a trunk branch is discovered, the following decision tree should be used to resolve it:

- Default to reverting the PR that caused the problem.
- Five minutes: Can the bug be fixed in under five minutes? Go for it. If not, revert the offending PR.
- One try: If fixing forward was already attempted and other issues were discovered in the process, revert all involved PRs.

### Request a new release

See our [deployment policies](https://depo-platform-documentation.scrollhelp.site/developer-docs/deployment-policies) for initiating a new production release from the given trunk branch.

> **Note:** The Platform rarely uses binary rollbacks (deploying previously-deployed versions) because of database migration risks and frontend-backend dependencies. Exceptions must exclude database migrations in the affected commit range. Exceptions are requested with the [out-of-band deploy policy](https://depo-platform-documentation.scrollhelp.site/developer-docs/deployment-policies#Requesting-out-of-band-deploys).

### Platform and VFS engineer roles and responsibilities

Platform code is divided into two categories: common code and application code.

1. Common code comprises behavior and functionality that's shared across applications.
2. Application code provides specific functionality for a VFS application.

Platform engineers are responsible for maintenance, detecting bugs, and performance in common code and libraries. VFS application teams are responsible for the quality of their FE and BE application code.

[Continue](./4-code-of-conduct.md)

[Back](./2-welcome.md)
