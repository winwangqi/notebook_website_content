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
