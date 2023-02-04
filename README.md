# 低碳课题的数据库开发项目

### 任务一：

基于python语言用Tkinter完成了数据导入导出程序的开发，实现txt和excel文件互换的功能以及excel数据上传数据库时设置配置文件并给出如列名是否存在 ，个别必空字段 、必填字段 、字段长度限制， 时间格式规范是否合法等具体规范修改反馈。

![image](https://user-images.githubusercontent.com/60246446/216748544-71950d90-f19f-4b83-a6b7-bddcb1b73525.png)


软件说明：

该软件总体分为俩个渠道，一个无限制条件直接转化，另一个需上传配置文件（需确保excel列名和配置文件中的列名及表名一致），然后检测，输出检测结果。
使用效果：

![image-20230204121916264](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230204121916264.png)



### 任务二：

个性化相似项目推荐算法分为两步，文本编码与相似度计算。文本编码采用了两种方法对领域长文本进行处理，第一种方法先提取了文档中的动词 、名词和形容词 ，并将词语变形归一作为文档的文本信息 ，再借助glove向量提取文本向量特征 ；另一种方法先做了数据预处理 ，通过KeyBERT提取数据摘要 ，喂入Bert-scincl预训练模型实现编码；最后分别将编码结果进行余弦距离相似度计算，展示出最相似的10个项目，完成个性化相似项目推荐算法。

#### **文本相似度计算-基于spacy和word2vec**

##### 1、输入输出

输入：project_id，project_title，objective字段。

输出：JSON格式，output中查看

[{"id": 821461, "title": "Pilot ......", "objective": "As the .........",

"sim_project": [{"id": 316919, "title": "Education......", "objective": "..............", "value": 0.9531599138669087}, 

{"id": 286801, "title": "..........", "objective": "..........", "value": 0.9513638158656776}, 

..............(10个)]

}]

 

##### 2、使用

通过检索输出的json结果文件sim_project中的id来实现相似度查询。可以将计算出来的文档向量另存为txt文档保存，定期更新，每次查询计算相似度。

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml11764\wps1.jpg) 

  

##### 3、算法主要思想

对文档进行预处理，为了对文档进行精确描述，提取文档中的动词、名词、和形容词，

并将词语变形归一，来作为文档的文本信息，然后借助glove向量提取文本向量特征。最后

计算文本相似度。

 

##### 4、本地环境配置

python 3.8

pip install spacy==3.2

pip install en_core_web_lg-3.2.0-py3-none-any.whl

glove.6B.300d.txt 预训练词向量文件放在运行代码的路径下，用于调用计算词向量。

 

##### 5、本地代码运行(colab会快很多)

Python  基于spacy和word2vec计算相似度.ipynb

 

#### **基于摘要的bert相似度计算**

##### 1、输入输出

输入：project_id，project_title，objective字段。

输出：txt结果文档（可转化为一个Excel的多个sheet输出，也可直接以id检索提取），output中查看：

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml11764\wps2.jpg) 

 

##### 2、使用

通过对txt结果进行数据框的转化，实现excel的输出。

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml11764\wps3.jpg) 

 

##### 3、算法主要思想

数据预处理：去除空值，全部转化为小写，去除标点符号。通过KeyBERT(model='all-mpnet-base-v2')模型提取摘要。

摘要结果如下：

{'737929': 'disruptive innovation refrigeration,innovation refrigeration,innovation refrigeration systems,cold energy management,industries refrigeration systems,industry conventional refrigeration,energy efficiency refrigeration,industries refrigeration,refrigeration appliances achieving,efficiency refrigeration appliances'},

然后将其摘要代表项目，放入scincl模型进行编码和相似度计算。

 

##### 4、本地环境配置

pip install pyhanlp 

pip install transformers

pip install sentence_transformers

all-mpnet-base-v2，scincl文件夹放在运行代码的路径下，分别用作摘要提取和相似度计算。

stopwords_en.txt 停用词表放在运行代码的路径下，用于去停用词，该词表也可以自己添加或删除词语。

 

##### 5、代码运行(colab会快很多)

Python  基于摘要的bert相似度计算.ipynb
