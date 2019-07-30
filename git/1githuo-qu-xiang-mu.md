# 取得项目的 Git 仓库
第一种是在现存的目录下，通过导入所有文件来创建新的 Git 仓库
第二种是从已有的 Git 仓库克隆出一个新的镜像仓库来

# 现存目录
- git init
- git add *.c
- git add README
- git commit -m 'initial project version'

# 克隆

git clone git://github.com/schacon/grit.git

git clone git://github.com/schacon/grit.git mygrit    别名