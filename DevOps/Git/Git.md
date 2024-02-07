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