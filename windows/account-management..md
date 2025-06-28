# Account management

- [Disable a user account](#disable-user-account)

## Disable a user account

To disable a user account, we use ways as:

- Using Command Prompt: `net user <username> /active:no`.
- Using Computer Management window, navigate to System Tools > Local Users and Groups > Users.
- Using `wmic` command: `wmic useraccount where name='user-name' set disabled=true`.

```cmd
net user <username> /active:no
```

works fine, if username is like Johm, Mike, etc.

If username is like Jo Ann M. Jones, Albert.David or any typical name, the command doesn’t work successfully. Mostly it shows error,
even with commands like:

```cmd
net user "Jo Ann M. Jones" /active:no
```

or

```cmd
net user 'Jo Ann M. Jones' /active:no
```

**Source:** [Microsoft Learn](https://learn.microsoft.com/en-us/answers/questions/1019807/disable-user-account-in-windows-10-and-windows-11).

