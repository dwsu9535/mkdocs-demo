# 项目文档

## 项目介绍
静态文档网站生成器Zensical创建静态文档站点Demo

## 安装zensical和初始化
```
使用uv安装zensical

uv init <项目目录>
uv venv .venv
uv add zensical
source .venv/bin/activate

zensical new .
zensical serve

参考文档
https://zensical.org/docs/get-started/
```

## 配置GitHub Pages
```
仓库设置
在仓库的Settings中，找到Pages选项，Build and deployment->Source选择GitHub Actions

编辑并提交.github/workflows/docs.yml

name: Documentation
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/configure-pages@v5
      - uses: actions/checkout@v5
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: pip install zensical
      - run: zensical build --clean
      - uses: actions/upload-pages-artifact@v4
        with:
          path: site
      - uses: actions/deploy-pages@v4

提交并推送
git commit -a -m "Add GitHub Actions workflow for docs"
git push

查看部署状态
GitHub仓库->Actions中查看部署状态 绿色打钩说明部署成功

静态文档站点地址
https://<用户名>.github.io/<仓库名>/
https://dwsu9535.github.io/mkdocs-demo/
```
