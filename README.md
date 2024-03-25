# github-release-management

A repo to play with release managment using github.

See [the workflow](./.github/workflows/deployment-pipeline.yaml) for the definition of the release pipeline.

See [repository actions](https://github.com/xpcoffee/github-release-management/actions) for the releases end up looking.

## Things tried, which work

 - Waiting before deploying to more environments.
   - Fake environment called a "gate" is used and a timer is set for that environment.
   - Timer can be bypassed if needed.
   - Next wave of environments after the gate then get deployed.
   - Could potentially use to wait for enough data/metrics/errors, then have validation step to check that data is healthy before moving on.
 - Not auto-cancelling previous deployments (especially if there's a wait stage). Let a change fully deploy before doing the next one.
   - If a change is already going, the next one will wait in a queue
   - Only the latest change in a queue gets promoted (changes in the queue that haven't started deploying get superceded by a new change)
 - Tagging commits as they get deployed. Not sure how useful this is if there's a large change set; only latest commit gets tagged.
 
 ## Things tried, that weren't useful
 
 - Using github releases to track a changeset.
   - These are meant to package your change so that it can be downloaded or published elsewhere. It's not useful for release management.  

 ## Don't know how to do this yet

 - Automatic rollbacks if an error is detected
 - Blocking a pipeline until an issue is fixed (other than disabling the action altogether)
