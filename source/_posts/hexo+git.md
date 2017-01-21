# **思路**
---
- master分支存放hexo生成的静态网页，hexo分支存放源码。
- 修改博客时操作master分支
- 修改主题，更换电脑时操作hexo分支

# **构建步骤**
---
- 当前目录执行博客初始化操作
  - $ hexo init
  - $ npm install
  - 此时博客已经初始化完毕，测试：
    - $ hexo g //生成静态页面
    - $ hexo server //启动服务器验证
    - 浏览器输入localhost:4000验证
  - 此时 master分支信息被消除[应该是hexo init的原因]
  - 额外的，为了执行hexo d命令需要安装：
    - $ npm install hexo-deployer-git --save
- 修改当前目录下的`_config.yml`文件，会使得**public文件夹**[ 即生成的静态页面 ]和repo中填写的代码仓库相关联
  - 修改内容如下：
    - type: git
    - repo: [address]
    - branch: master
  - 注：冒号后面**必须**有空格
- $ hexo d
  - 将 public文件夹 提交到 远程master分支
- 接下来需要将源码提交到远程的hexo分支[当前远程并没有hexo分支]：
  - $ git init
    - 初始化git信息，执行结束可看到master标记
  - $ git remote add origin [仓库地址]
    - 当前代码与远程仓库关联
  - $ git add .
  - $ git commit -m "注释信息"
    - 注：当前操作是在本地master分支
  - $ git push origin master:hexo
    - 该命令会在远程自动创建hexo分支
  - 验证：github仓库中可看到新的分支的代码

# **更换设备**
---
`$ git clone [repertory]`
`$ git checkout -b hexo origin/hexo`
> 认准分支，其他的都很简单
