
# 工程准备

```
# First, clone the repo via git:
git clone --depth=1 https://github.com/electron-react-boilerplate/electron-react-boilerplate.git recess

cd recess

# remove git info, in order to commit to your git hub
rm -rf .git

# git init
git init
git status
git add *
git commit -m "init"
git remote add origin https://github.com/dragon-distributed/recess.git
git push -u origin master

```

# vs code 准备

```
https://code.visualstudio.com

安装插件

https://electron-react-boilerplate.js.org/docs/editor-configuration

code --install-extension dbaeumer.vscode-eslint
code --install-extension dzannotti.vscode-babel-coloring
code --install-extension EditorConfig.EditorConfig
code --install-extension flowtype.flow-for-vscode

不知道怎么做，就可以在
code->首选项->extensions，
搜索dbaeumer.vscode-eslint，dzannotti.vscode-babel-coloring等等

```


# 遮掩的窗口

```
安装material-ui, 
1. 在package.json，在dependencies中，添加material-ui/core，提一下，这里的^是指大于这个版本都行。@不是什么特殊符号，只是包是这个命名。
"@material-ui/core": "^4.8.0",

yarn install
```

```
1. 
```

