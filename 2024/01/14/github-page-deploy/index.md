# Github Action 自动部署发布


## 1. 创建两个仓库

一个用来存放 Hugo 源文件，私有、公有都可以

一个用来托管网站，用户名.github.io



## 2. 生成部署密钥

```
ssh-keygen -t rsa -b 4096 -C user.email
```

这种方式可以输入自定义的路径来保存SSH Key，这样就不会影响到电脑中旧的SSH Key。

生成过程中要输入生成密钥路径：`/xx/xx/.ssh/id_rsa_hugo_deploy`  

```
id_rsa_hugo_deploy.pub (public key)
id_rsa_hugo_deploy     (private key)
```



## 3. 填写密钥

将 **Public Key** 填写到username.github.io

点击 Settings，再点击Deploy keys，填写 Public Key

记得勾上 `Allow write access`



将 **Private Key** 添加到 Hugo 源文件仓库

点击 Settings，再点击 Secrets，填写 Private Key

变量名要复制下来，一会儿要用



## 4. 编写 Github Actions 脚本

为 Hugo 源文件仓库配置 Actions

```yaml
name: Hugo Github Pages
on:
  push: # push 的时候触发
     branches: # 分支触发
      - main
jobs:
  build:
    runs-on: ubuntu-latest # 镜像市场
    steps:
      - name: checkout
        uses: actions/checkout@master #软件市场的名称
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true
      - name: Build # 编译
        run: hugo --minify
      - name: Deploy # 部署
        uses: peaceiris/actions-gh-pages@v2
        env:
         ACTIONS_DEPLOY_KEY: ${{ secrets.HUGO_SECRET_NAME }} #用到 secrets变量名
         EXTERNAL_REPOSITORY: username/username.github.io
         PUBLISH_BRANCH: main
         PUBLISH_DIR: ./public
```


