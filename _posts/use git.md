## git使用及上传到GitHub

# 1.安装git
 windows: Git Bash
 linux:sudo apt-get install git  
 
 # 2. 设置ssh
$ git config --global user.name "Your Name" 
$ git config --global user.email "email@example.com"  
 
 
 mkdir .ssh  
 cd .ssh  
 ssh-keygen -t rsa -C "youremail@example.com"      
 id_rsa和id_rsa.pub ，把公钥拷贝到GitHub-setting-ssh key -add ssh   
 
  # 3.创建git本地仓库
  cd到项目文件夹下，  
  git init   
  git add readme.txt    
  git add ./xxx/xxx.cpp    
  git commit -m "first commit"    
  
  排除不添加部分   
  git status,拷贝不需要添加的列表    
  vim .gitignore  
  
  git log 参看commit的多次版本  
  
  # 4.远程仓库  
  ## 创建远程仓库  
  github--new repository,创建与本地仓库相同的名字的仓库，并做相关设置。 
  “Quick setup — if you’ve done this kind of thing before”选择ssh,不要选择htttp,否则上传时需要输入用户名和密码  
  并按提示把本地仓库链接到远程仓库,…or push an existing repository from the command line
  ```  
  git remote add origin git@github.com:weogen/***.git
  git branch -M master
  git push -u origin master
  ```  
  
  
  //由于master的歧义歧视，官方已经改为main  
  git push -u origin master  
  git pull origin master  
 
 # git问题error: remote origin already exists.  
 取消关联：git remote rm origin  
 # ERROR: You're using an RSA key with SHA-1, which is no longer allowed. Please use a newer client or a different key type.  
 
 github不再支持SHA-1的加密方式了。  
将SHA-1的加密方式修改为ECDSA的方式，并把公钥加入到github中，具体操作步骤如下。  
ssh-keygen -t ecdsa -b 521 -C "your_email@example.com"  
 
 # 另一台设备  
  设置与上述相同,关联相同  
  直接pull 
  git pull <远程主机名> <远程分支名>:<本地分支名>  
  git pull origin master:brantest  

  将远程主机origin的master分支拉取过来，与本地的brantest分支合并。
  后面的冒号可以省略：
  git pull origin master  
 
 
 
