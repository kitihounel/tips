# shell

- [Ctrl-C and Ctrl-Z](#ctrl-c-and-ctrl-z)

## Ctrl-C and Ctrl-Z

If we leave edge cases to one side, the difference is simple. Ctrl+C aborts the application almost immediately while Control+Z shunts it into the background, suspended.

The shell send different signals to the underlying applications on these combinations:

- `Ctrl+C` (control character **intr**) sends SIGINT which will interrupt the application. Usually causing it to abort, but this is up to the application to decide.

- `Ctrl+Z` (control character **susp**) sends SIGTSTP to a foreground application, effectively putting it in the background suspended. This is useful if you need to break out of something like an editor to go and grab some data you needed. You can go back into the application by running **fg** (or **%x** where **x** is the job number as shown in **jobs**).

  We can test this by running `nano foo.txt`, then pressing Control+Z and then running `ps aux | grep foo`. This will show us the nano process is still running:

  ```sh
  oli     3278  0.0  0.0  14492  3160 pts/4    T    13:59   0:00 nano foo.txt
  ```

  Further, we can see (from that T, which is in the status column) that the process has been stopped. So it's still alive, but it's not running... It can be resumed.

  Some applications will crash if they have ongoing external processes (like a web request) that might timeout while they're asleep.

it's also possible to run `bg` (instead of `fg`) to unsuspend an application that's been Ctrl+Z'ed without putting it back into the foreground; effectively giving you control of both the shell that started the application and the application itself, as if you had used `&` when starting the application. This often comes in handy when you forgot to start it with `&`.

Source: https://askubuntu.com/questions/510811/what-is-the-difference-between-ctrl-z-and-ctrl-c-in-the-terminal
