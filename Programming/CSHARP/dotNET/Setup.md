# Manjaro Setup
[[dotNET]] Manjaro [[Linux]] setup

## With source and script intallation:

```bash
wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
chmod +x ./dotnet-install.sh
./dotnet-install.sh --version latest
``` 
Suggestion: install at in `/usr/share/dotnet` folder. After installation, this should have `dotnet` binary file.

Finally put this lines in `.zshrc` to load `dotnet` root path and tools to environment variables.
`.dotnet/tools` will store the installation of things like language server and other tools related with dotnet.
```bash
export DOTNET_ROOT=/usr/share/dotnet
export PATH=$PATH:$DOTNET_ROOT
export PATH="$PATH:/home/vinico/.dotnet/tools"
```
