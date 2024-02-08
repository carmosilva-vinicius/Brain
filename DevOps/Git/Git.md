Git is a free and open-source **version control system (VCS)**, meaning it tracks changes made to files, typically code, over time. Think of it as a time machine for your code: you can see who changed what, when, and why, and even revert back to older versions if needed.

How does Git fit into the [[DevOps]] area?
- **Source code management:** Git serves as the foundation for collaborative development in DevOps. Teams use it to share code, track progress, and ensure everyone is working on the same version.
- **Continuous integration and continuous delivery (CI/CD):** CI/CD pipelines automate building, testing, and deploying code changes. Git integrates seamlessly with CI/CD tools, enabling automated version control throughout the delivery process.
- **Configuration management:** Git can also store and manage infrastructure configuration as code, allowing infrastructure to be treated like software and provisioned automatically for consistent and repeatable deployments.

Key features of Git include:

- **Version history:** Keeps a complete record of every change made to files, allowing you to trace the evolution of your project.
- **Branching:** Create parallel versions of your codebase to experiment with new features or fix bugs without affecting the main project.
- **Merging:** Combine changes from different branches into the main project when satisfied.
- **Collaboration:** Multiple developers can work on the same project simultaneously, with Git ensuring changes don't conflict.
## Global config
```sh
$ git config --global user.name "Fulano de Tal"
$ git config --global user.email fulanodetal@exemplo.br
```
## Local config
```sh
$ git config --local user.name "Fulano de Tal"
$ git config --local user.email fulanodetal@exemplo.br
```
### Adding tracked files to .gitignore

The **`.gitignore`** file only affects untracked files. Once a file has been committed, it is part of the Git history and will continue to be tracked unless you explicitly remove it from the repository's history:

```sh
$ git rm -r --cached <file-path>
$ git commit -m "Stop tracking files in <file-path> folder"
```