# Configuration

Configuration can be applied at three different levels
- System level - apply to all users
- Global level - apply to all repositories of the current user
- Local level - apply to the repository of the current folder

## Initial configuration

1. From the home directory we start by setting the username:
```bash
git config --global user.name "Your name"
```

2. Next, we set email:
```bash
git config --global user.email your@email.com
```

3. Set the default editor:
```bash
git config --global core.editor "code --wait"
```

4. Configure end of line 

|                 | Windows                                   | Mac              |
| --------------- | ----------------------------------------- | ---------------- |
| End of line     | `\r` `\n` (Carriage Return and Line Feed) | `\n` (Line feed) |
| `core.autocrlf` | `true`                                    | `input`          |
Set Git to handle carriage return removal/addition for multi-OS contributions.
I'll set `core.autocrlf` to `input` since I am on MacOS
```bash
git config --global core.autocrlf input
```

5. If we need some help with the configuration:
```bash
git config --help
```

```bash
git config -h
```

## Set VSCode a the diff tool
```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```


## Edit configuration
Run this command to edit the global configuration
```bash
git config --global -e
```

