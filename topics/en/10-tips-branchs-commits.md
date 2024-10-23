# Tips for creating branches and commits
A tip for you who are unsure of what to add to your commit and how to name a branch.

### Commits
Here are some tips for you who are in doubt about how to name your commits:

- **Feat**: Used when you are adding a new feature.
  - Example: `feat: add login functionality`

- **Fix**: Used to fix a bug or error.
  - Example: `fix: fix authentication error`

- **Style**: Used for formatting changes, such as spacing or code style, without changing the logic.
  - Example: `style: adjust spacing on buttons`

- **Refactor**: Used to refactor code without adding new features or fixing bugs.
  - Example: `refactor: reorganize user module`

- Revert: Used to revert previous commits.
  - Example: `revert: revert dependency change`

- **Delete**: Used to remove code, files or dependencies that are no longer needed.
  - Example: `delete: remove deprecated module`

- Update: Used for minor updates, such as to documentation or dependencies.
  - Example: `update: update README`

- **Build**: Used for changes to the build system or dependencies.
  - Example: `build: update Webpack configuration`

- **Config**: Used for changes to application or environment settings.
  - Example: `config: adjust environment variables`

- Chore: Used for minor or maintenance tasks that do not change the source code directly.
  - Example: `chore: clean up unused files`

- **CI**: Used for changes to the continuous integration configuration.
  - Example: `ci: adjust GitHub Actions pipeline`

- **Docs**: Used for changes or adding documentation.
  - Example: `docs: add API usage examples`

- **Perf**: Used for performance optimizations.
  - Example: `perf: improve database query performance`

- **Test**: Used to add or modify tests.
  - Example: `test: add unit tests for login module`

# Branches and Git Flow
In Git Flow, the branches follow a defined structure to organize the development flow. Here are tips on how to name the branches within this flow:

- **Feat**: Used to add a new feature. Usually created from the `develop` branch.
  - Example: `feature/new-functionality-login`

- **Fix and Hotfix**: Used to fix bugs or errors. Usually created from `develop` or `hotfix` (if it's an urgent fix).
  - Example: `fix/fix-authentication-error` - `hotfix/fix-production-error`

- **Refactor**: Used to refactor code without changing functionality. Created from `develop`.
  - Example: `refactor/reorganize-module-user` 

- **Release**: Used to prepare a new version of the code, usually created from `develop` and then merged into `main` and `develop`.
  - Example: `release/1.0.0`
