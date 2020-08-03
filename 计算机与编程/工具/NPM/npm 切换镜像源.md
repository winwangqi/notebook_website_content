# NPM 切换镜像源

## 配置 `config`

```bash
npm config set registry https://registry.npm.taobao.org
```

## 命令行指定

```bash
npm --registry https://registry.npm.taobao.org info underscore 
```

## 编辑 `~/.npmrc`

```text
registry = https://registry.npm.taobao.org
```
