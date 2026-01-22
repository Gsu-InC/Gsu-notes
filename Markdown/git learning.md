# git学习日记
## 一个标准的、规范化的Git工作流程：
修改文件 → 暂存更改(add) → 提交更改(commit) → 同步远程(pull/push)
## 命令
```
git config --global user.name
git config --global user.email
git config --global --list 查看全局配置

git init
git remote add origin your_link
git branch -M main
echo "# Hello world" > README.md
git add . # 进入文件夹再用这个，不然会跳一堆乱七八糟的东西，也可以直接git add +你修改过的文件名
git commit -m "first commit" #提交add里的东西到本地仓库中并附带“”中的信息
git push -u o



rigin main 
```

```
git status # 查看状态
git ls-files #查看被跟踪文件 
git check-ignore -v 文件名 查看是否被.gitignore 忽略，有输出则是，没有则没被忽略
```
### 远程仓库相关
```
git remote -v # 查看远程仓库地址
git remote # 仅列出远程仓库简称
git remote get-url origin # 获取简称origin对应的具体URL
git remote show origin # 显示origin远程仓库的详细信息（包括分支跟踪关系）
git remote set-url origin <新仓库地址> # 更改origin指向的地址
git remote set-url origin git@github.com:你的用户名/你的仓库.git # 修改地址味SSH格式，便于配置免密钥登陆
# 注意，操作后务必再运行git remote -v 查看是否修改正确
```
### 从github上抓取项目
```
git pull origin main # 拉取主项目到本地
git pull origin main --allow-unrelated-histories # 允许合并不相关历史
```
### 解决冲突
- 已解决冲突，添加文件并提交
```
git add .
git commit -m "Merge Resolved"
```
- 放弃合并
```
git merge --abort
```
- 继续合并
```
git merge --continue
```
- 储藏当前未提交的更改
```
git stash
```
- 恢复储藏的更改
```
git stash pop
```
- 查看详细的合并状态
```
git log --merge 
```
- 流程总结

1. 查看状态
```git status```

2. 解决文件中的冲突（比如编辑app.js）
   1. vi 进入文件并删除<<< === >>> 类乱码
   2. :wq保存
3. 添加解决后的文件
```git add app.js```

1. 完成合并提交
```git commit -m "解决合并冲突"```
### 推送被拒绝
```git pull --rebase origin main  # 先拉取并变基```

### clone
```
git clone 克隆仓库链接
```

### pull request
