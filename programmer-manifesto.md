# The Programmer's Manifesto

## Code collaboration

  1. Don't check in broken code
  2. Refactoring time is a myth--once a PR is closed the code should be assumed to be final.
  3. Don't check in commented code
  4. Don't make breaking changes (without informing the team)
  5. Don't add authors names to code, we have Git Blame for that, vanity not needed
  6. Work in a fork or a branch and integrate code with PRs

### Code Reviews

  1. Does the code compile?
  2. Does it pass all existing unit tests?
  3. Is all new functionality fully unit-tested?
  4. Is all commented code removed?
  5. Are all modified files formatted using the correct formatter?
  6. Is this the simplest, cleanest verison of this code?