# github 搜索技巧




[github 官方文档](https://docs.github.com/zh)



## 常用搜索语法

### in 限定搜索范围

可以限定范围去找 github 仓库

| 限定符            | 示例                                                         |
| :---------------- | :----------------------------------------------------------- |
| `in:name`         | [**jquery in:name**](https://github.com/search?q=jquery+in%3Aname&type=Repositories) 匹配名称中带有“jquery”的存储库。 |
| `in:description`  | [**jquery in:name,description**](https://github.com/search?q=jquery+in%3Aname%2Cdescription&type=Repositories) 匹配名称或说明中带有“jquery”的存储库。 |
| `in:topics`       | [jquery in:topics](https://github.com/search?q=jquery+in%3Atopics&type=Repositories) 将带“jquery”标签的存储库匹配为主题。 |
| `in:readme`       | [**jquery in:readme**](https://github.com/search?q=jquery+in%3Areadme&type=Repositories) 匹配自述文件中提及“jquery”的存储库。 |
| `repo:owner/name` | [**repo:octocat/hello-world**](https://github.com/search?q=repo%3Aoctocat%2Fhello-world) 匹配特定的存储库名称。 |

### 按照仓库创建或者上次更新时间搜素

找到当前活跃的仓库

| 限定符                              | 示例                                                         |
| :---------------------------------- | :----------------------------------------------------------- |
| `created:<*YYYY-MM-DD*`             | [**webos created:<2011-01-01**](https://github.com/search?q=webos+created%3A<2011-01-01&type=Repositories) 匹配具有 2011 年之前创建的“webos”一词的存储库。 |
| `pushed:>*YYYY-MM-DD*`              | [**css pushed:>2013-02-01**](https://github.com/search?utf8=✓&q=css+pushed%3A>2013-02-01&type=Repositories) 匹配具有在 2013 年 1 月之后推送到其中的“css”一词的存储库。 |
| `pushed:>=*YYYY-MM-DD*` `fork:only` | [**case pushed:>=2013-03-06 fork:only**](https://github.com/search?q=case+pushed%3A>%3D2013-03-06+fork%3Aonly&type=Repositories) 匹配在 2013 年 3 月 6 日或之后将“case”一词推送到其中的存储库（即分支）。 |

### 按照语言搜索

搜索特定的编程语言

| 限定符                | 示例                                                         |
| :-------------------- | :----------------------------------------------------------- |
| `language:*LANGUAGE*` | [**`rails language:javascript`** ](https://github.com/search?q=rails+language%3Ajavascript&type=Repositories)匹配具有以 JavaScript 编写的“rails”一词的存储库。 |



## 组合搜索

比如说我现在要寻找 api 开放平台


