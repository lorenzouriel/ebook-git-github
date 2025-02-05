# Tools and Integrations
## Git Integration with Popular IDEs
**1. VSCode:**
- VSCode has native integration with Git. You can initialize repositories, commit, pull, push, view commit histories, and resolve conflicts directly from the editor.

- There are several extensions, such as **GitLens**, that enhance the Git experience in VSCode, offering features such as viewing line authorship, comparing branches, and more.

**2. IntelliJ:**
- IntelliJ offers robust integration with Git, allowing you to manage repositories, commits, branches, merges, and more, directly from the IDE.

- Graphical tools for file comparison and merge conflict resolution are built in and quite intuitive.

## Using Graphical Tools for Git

**1. GitKraken:**
- Provides a clear visual interface for managing Git repositories, with features such as viewing commits, creating and managing branches, and resolving conflicts.

- Supports integrations with several repository hosting platforms such as GitHub, GitLab, Bitbucket, among others.

**2. SourceTree:**
- Allows you to clone, create, and manage local and remote repositories with an intuitive graphical interface.

- Provides a detailed view of the commit and branch history, making it easier to track changes.

## Integration with CI/CD
**1 Jenkins:**
- Jenkins can be configured to automatically start builds on Git events such as commits and pull requests.

- There are specific plugins for integrating with Git, which facilitate the monitoring of repositories and execution of pipelines.

**2. GitHub Actions:**
- Allows the creation of automated workflows that are triggered by Git events (push, pull request, etc.).

- Workflows are configured using YAML files, offering great flexibility and control over CI/CD processes.

**3. GitLab CI:**
- Defines CI/CD pipelines directly in the repository with `.gitlab-ci.yml` files.

- Deep native integration with the GitLab repository, offering advanced CI/CD features such as automatic build, test, and deploy.

## GitFlow
GitFlow is a branching model that defines an organized and efficient development process.

**Main branches:**
- `main`: Contains the production code.

- `develop`: Contains the code for the next version that will be released.

**Support branches:**
- `feature/*`: Used for developing new features.

- `release/*`: Preparation of a new production version.

- `hotfix/*`: Urgent fixes in production.