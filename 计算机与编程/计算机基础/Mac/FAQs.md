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

## [Compress files from terminal](https://superuser.com/questions/505034/compress-files-from-os-x-terminal)

```bash
zip [targetName] [fileNames]
```

example:

```bash
zip build202010230955 build/**/*
```

[How to compress and uncompress files and folders in the Terminal](https://coolestguidesontheplanet.com/how-to-compress-and-uncompress-files-and-folders-in-os-x-lion-10-7-using-terminal/)

## 查看端口占用，关闭进程

查看占用端口进程

```bash
lsof -i [PORT]
```

关闭进程

```bash
kill [PID]
```
