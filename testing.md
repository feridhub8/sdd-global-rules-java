# Testing

- Tests are written together with the feature they cover, in the same change and the same commit. A feature without its tests is not done.
- Verify behavior with automated tests, never with manual one-off checks (curl, scripts run by hand).
- Every spec scenario maps to at least one test. Tasks name the test that verifies them.
- Unit tests for logic, integration tests with Testcontainers for anything that talks to an external system (database, identity provider, secrets store).
- The assistant runs the test suite and reports the result; it does not repeat checks by hand.
