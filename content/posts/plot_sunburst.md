---
title: Plot_sunburst
subtitle:
date: 2024-12-06T09:16:13+08:00
draft: false
type: posts
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - Python绘图
categories:
  - Python绘图
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---
### 旭日图

> <font color='Black'>@ 旭日图也称为太阳图，是一种圆环镶接图。 </font> 

><font color='Black'>@ 旭日图中每个级别的数据通过1个圆环表示，离原点越近代表圆环级别越高，最内层的圆表示层次结构的顶级，然后一层一层去看数据的占比情况。越往外，级别越低，且分类越细。  </font>


{{< admonition type=abstract open=false title="sunburstplot" >}}

> <font color='Black'><b>@ Input file format</b></font>
```txt
A	B	C	D
Intergenic	None	None	835
3kb-promoter	None	None	1485
Genic	UTR	5_UTR	67
Genic	UTR	3_UTR	66
Genic	Intron	None	665
Genic	Exonic	Synonymous	219
Genic	Exonic	Missense	134
```

> <font color='Black'><b>@ Python script</b></font>
```py
#!/home/yuqing/bin/python
import sys
import plotly.graph_objects as go
import plotly.express as px
import plotly.offline as offline
import pandas as pd
df = pd.read_csv(sys.argv[1],sep='\t')
#df.fillna(None,inplace=True)
df=df.where(df.notnull(), None)
#df=df.convert_dtypes()
print(df)
fig = px.sunburst(df, path=['A','B','C'], values='D')
fig.write_image(f"{sys.argv[1]}.pdf")
offline.plot(fig, filename=f'{sys.argv[1]}.html', auto_open=False
```
{{< /admonition >}}

> <font color='Black'><b>@ 结果图展示</b></font>

<p align = 'center'>
<img src="/旭日图.png" width="500">  
</p>