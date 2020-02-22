
git常用的命令行
git clone https://github.com/wlz1244/qingoo.git   //下载一个master分支代码 
git branch wlz  //新建wlz分支
git checkout wlz  //切换到wlz分支
git pull origin dev //将远程dev分支更新到本地wlz分支
··············写代码
git add .
git commit -m "XXXXX"       //现在还是wlz分支
git checkout dev   //切换到dev分支
git pull origin dev  //将本地dev分支更新到最新远程dev分支，一摸一样
git merge wlz  //将本地wlz分支合并到本地最新dev分支
·············有冲突的话，解决冲突
// git add .
// git commit -m "XXXXX"
git push origin dev  //提交到远程dev分支
git checkout wlz  //切换到wlz分支
git pull origin dev //更新最新代码到本地
git reset --hard origin/dev      后退已经commit的东西到git服务器的最新代码