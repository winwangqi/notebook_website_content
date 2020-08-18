# Mac FAQs

## How can I extract .rar files on the Mac?

Using Homebrew, in a terminal type:

```bash
brew install unrar
```

to use it just navigate to your file and type

```bash
unrar x <filename>
```

## 查看端口占用，关闭进程

查看占用端口进程

```bash
lsof -i [PORT]
```

关闭进程

```bash
kill [PID]
```
