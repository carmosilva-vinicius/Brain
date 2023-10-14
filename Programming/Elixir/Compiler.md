In [[Elixir]] is a conventions to use `exs` file extension to scripting file, which will be just executing. But to files which will be compiled the extension should be `ex`.
To compile a f `ex`:
```
elixirc arquivos.ex
```
this will result in a `.beam` file, which is an executable to the Earlang Virtual Machine.

To run a Elixir script we can do:
```
elixir arquivos.exs
```
That will turn on the Earlang Virtual Machine, run the script and turn off.