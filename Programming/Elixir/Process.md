In [[Elixir]], all code runs inside processes. Processes are isolated from each other, run concurrent to one another, and communicate via message passing[0](https://elixir-lang.org/getting-started/processes.html). Processes in Elixir are extremely lightweight in terms of memory and CPU, even compared to threads in other programming languages[0](https://elixir-lang.org/getting-started/processes.html). Elixir processes are not the same as operating system processes; when a process is created in Elixir, it is actually created within the Erlang Virtual Machine (BEAM) as a lightweight internal structure[2](https://cratecode.com/info/elixir-processes-message-passing).

We can use `spawn` to create a new process. Elixir also have the `Process`module to manage them, like check if its alive. `self()` checks the current process.
```rb
iex(1)> spawn(fn -> IO.puts("Estou em outro processo") end)
Estou em outro processo
#PID<0.111.0>
iex(2)> IO.puts("Estou em outro processo")
Estou em outro processo
:ok
iex(3)> pid = spawn(fn -> IO.puts("Estou em outro processo") end)
Estou em outro processo
#PID<0.112.0>
iex(4)> Process.alive?(pid)
false
iex(5)> self()
#PID<0.110.0>
```

### Communication

We can use `receive` to maintain a process alive, until it receive a message. `send(pid, "message example")` is used to send a message to specific process which is awaiting for a message. After receive the process is turned off.
```rb
iex(1)> pid = spawn(fn -> receive do 
...(1)> conteudo -> IO.puts(conteudo)
...(1)> end
...(1)> end
...(1)> )
#PID<0.111.0>
iex(2)> pid
#PID<0.111.0>
iex(3)> Process.alive?(self())
true
iex(4)> Process.alive?(pid)   
true
iex(5)> send(pid, "Texto para exibir no processo filho")
Texto para exibir no processo filho
"Texto para exibir no processo filho"
iex(6)> send(pid, "Texto para exibir no processo filho")
"Texto para exibir no processo filho"
iex(7)> Process.alive?(pid)
false
iex(8)>
```

When we send data to a process and it is not awaiting, the data will be stored in a kind of mailbox. So when we start the receive it will be read. But if we try to read and there is no message in the mailbox, the process will be block and awaiting.
```rb
iex(9)> send(self(), {:ok, "Mensagem de sucesso"})          
{:ok, "Mensagem de sucesso"}
iex(10)> IO.puts("Meu processo está destrvado")
Meu processo está destrvado
:ok
iex(11)> receive do
...(11)> {:ok, conteudo} -> IO.puts(conteudo)
...(11)> end
Mensagem de sucesso
:ok
iex(12)> receive do
...(12)> {:ok, conteudo} -> IO.puts(conteudo)
...(12)> end
```

### Timeout
On the other hand we can set a timeout expiration timer
```rb
iex(1)> receive do
...(1)> qualquer_coisa -> IO.puts(qualquer_coisa)
...(1)> after
...(1)> 1000 -> IO.puts("Timeout") 
...(1)> end
Timeout
:ok
```
