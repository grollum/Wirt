# Testing

Testing in this app should mostly be focussed around integration testing using [nightwatchjs](https://nightwatchjs.org).
When you see a complex function though, a unit test using [jest](https://jestjs.io/) is appreciated to ensure it does what it should!

All integration tests are in the `tests` directory and each file should represent one flow in the application!
An example for a flow would be:

- `I want to add a new device to my network` -> `using ipv6`, `using ipv4`
- `I want to update my server` -> `with a new hostname`

Make sure to test failures as you main objective! For example ensuring that adding devices with invalid data will fail!
Usually code is developed for the best case flow, these tests are what makes things safe and correct!
