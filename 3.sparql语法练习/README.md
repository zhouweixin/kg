# sparql 语法学习
---

## 1. 安装apache-jena-fuseki-3.7.0

### 1.1 下载

进入[官网](http://jena.apache.org/download/index.cgi)下载apache-jena-fuseki-3.7.0.zip, 如下图所示

![](images/01.png)

### 1.2 解压

打工目录如下图

![](images/02.png)

### 1.3 运行

双击fuseki-server.bat启动服务器

![](images/03.png)

打开浏览器输入http://localhost:3030访问

![](images/04.png)

### 1.4 创建数据集

点击如上图所示的Add one或者如下图所示添加数据集, 名为test

![](images/05.png)

## 2. 导入数据

### 2.1 创建RDF三元组文件: data1.nt

注: 三元组最后有一个 **"."**

data1.nt

```nt
<http://zhou.org/西游记/孙悟空> <http://zhou.org/名号> "齐天大圣" .
<http://zhou.org/西游记/通臂猿猴> <http://zhou.org/名号> "超天大圣" .
```

### 2.2 导入文件

![](images/10.png)

## 3. 查询命令

### 3.1 查询所有三元组

**查询语句:**
```sparql
select ?s ?p ?o
where{
	?s ?p ?o
}
```

**说明:**
- ?s, ?p, ?o表示变量, 查询语句里的变量都是以?开头
- ?s, ?p, ?o里的s, p, o表示的是变量名, 任何字母都可以
- select 后的?s, ?p, ?o无法确定表示什么含义, where里面的?s, ?p, ?o按顺序分别表示主, 谓, 宾, 使select后面的变量确定了含义
- where的语句要用{}包围
- where语句里内容表示的是匹配的含义, 此处全为变量, 表示匹配所有

**查询结果:**

```
{
  "head": {
    "vars": [ "s" , "p" , "o" ]
  } ,
  "results": {
    "bindings": [
      {
        "s": { "type": "uri" , "value": "http://zhou.org/西游记/孙悟空" } ,
        "p": { "type": "uri" , "value": "http://zhou.org/名号" } ,
        "o": { "type": "literal" , "value": "齐天大圣" }
      } ,
      {
        "s": { "type": "uri" , "value": "http://zhou.org/西游记/通臂猿猴" } ,
        "p": { "type": "uri" , "value": "http://zhou.org/名号" } ,
        "o": { "type": "literal" , "value": "超天大圣" }
      }
    ]
  }
}
```

**过程如下图:**

![](images/11.png)

### 3.2 查询孙悟空的名号

**查询语句**
```sparql
select ?名号
where{
	<http://zhou.org/西游记/孙悟空> <http://zhou.org/名号> ?名号
}
```

**结果**

![](images/12.png)

### 3.3 查询所有的名号

**查询语句**
```sparql
select ?名号
where{
	?s <http://zhou.org/名号> ?名号
}
```

**结果**

![](images/13.png)

### 3.4 带前缀的查询

**查询语句**
```
PREFIX 西游记: <http://zhou.org/西游记/>

select ?名号
where{
	西游记:通臂猿猴 ?p ?名号
}
```

**结果**

![](images/14.png)

## 未完待续...
