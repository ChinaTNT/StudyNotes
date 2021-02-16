> python

+ python 源慢解决方法

```python
pip install django -i https://pypi.tuna.tsinghua.edu.cn/simple
其他镜像
https://mirrors.aliyun.com/pypi/simple/
http://pypi.doubanio.com/simple/

```

+ 列表拉成一列

```python
from compiler.ast import flatten
listA = flatten([mulitlist]) #mulitlist可以为多层嵌套列表
```

> Git

+ 删除上次提交，使用reset命令

  HEAD是指向最新的提交，上一次提交是HEAD^,上上次是HEAD^^,也可以写成HEAD～2 ,依次类推。

```
git reset --hard HEAD^
git push origin master -f
```

> Markdown

+ 文件名中含空格无法在github中显示超链接，可以用\&#32;替代空格

  ![](链接失效.png)

  ```
  eg [Flask Web开发实战](Web基础/Flask&#32;Web开发实战.md)
  ```

  

> Github

```
# 解决GitHub图片不显示问题
# GitHub Start 
192.30.253.112    Build software better, together 
192.30.253.119    gist.github.com
151.101.184.133    assets-cdn.github.com
151.101.184.133    raw.githubusercontent.com
151.101.184.133    gist.githubusercontent.com
151.101.184.133    cloud.githubusercontent.com
151.101.184.133    camo.githubusercontent.com
151.101.184.133    avatars0.githubusercontent.com
#151.101.184.133    avatars1.githubusercontent.com
151.101.100.133    avatars1.githubusercontent.com
151.101.184.133    avatars2.githubusercontent.com
151.101.184.133    avatars3.githubusercontent.com
151.101.184.133    avatars4.githubusercontent.com
151.101.184.133    avatars5.githubusercontent.com
151.101.184.133    avatars6.githubusercontent.com
151.101.184.133    avatars7.githubusercontent.com
151.101.184.133    avatars8.githubusercontent.com

 # GitHub End
```

