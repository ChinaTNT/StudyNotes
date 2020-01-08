> python

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

