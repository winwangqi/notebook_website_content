# NPM FAQs

## 切换镜像源

### 配置 `config`

```bash
npm config set registry https://registry.npm.taobao.org
```

### 命令行指定

```bash
npm --registry https://registry.npm.taobao.org info underscore 
```

### 编辑 `~/.npmrc`

```text
registry = https://registry.npm.taobao.org
```


## 批量升级包到最新版本

```bash
npm i -g npm-check-updates
ncu -u
npm install
```

[ref](https://stackoverflow.com/questions/16073603/how-to-update-each-dependency-in-package-json-to-the-latest-version)


## 私有仓库

- [verdaccio](https://github.com/verdaccio/verdaccio)


## `npm i -g [pkg]` permission denied

- [Error: EACCES: permission denied, access '/usr/local/lib/node_modules'](https://stackoverflow.com/questions/48910876/error-eacces-permission-denied-access-usr-local-lib-node-modules)
- [NPM Install - Resolving EACCES Permissions Denied](https://letscodepare.com/blog/npm-resolving-eacces-permissions-denied)
- [How to fix npm throwing error without sudo](https://stackoverflow.com/questions/16151018/how-to-fix-npm-throwing-error-without-sudo)

first check who owns the directory

```bash
ls -la /usr/local/lib/node_modules
```

then change the directory owner

```bash
sudo chown -R $USER /usr/local/lib/node_modules
```
