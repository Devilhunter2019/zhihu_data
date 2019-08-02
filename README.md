# 2019年7月知乎大 V 数据分析
## 项目内容
* 抓取知乎粉丝数一万以上用户个人信息，包括回答数、文章数、粉丝数、获得收藏数、获得赞同数、收录文章数、收录回答数、关注的收藏夹、专栏；及粉丝数 10w 以上用户回答及文章详细信息；
* 根据知乎高关注度用户基本数据进行数据可视化分析，绘制图表包括：
   1. 用户回答数、文章数、粉丝数等排名；
   2. 用户回答数、点赞数、粉丝数散点图；
   3. 粉丝数前 50 用户关系图；
   4. 10w 粉丝用户回答、文章随时间变化图；
   5. 用户信息词云。
## 项目思路
1. 知乎是以回答为主的知识社区，为分析知乎高关注用户的基本情况，从高关注用户**张佳玮**关注用户开始抓取粉丝数 1w 以上用户，并以此类推，直至抓取完毕；为获得回答数、粉丝数、点赞数等相关排名。依据**获取的用户数据**抓取知乎粉丝数 1w 以上用户主页文章、回答、获得赞同数等数据及详细的回答、文章数据；
2. 使用 scrapy 分别抓取用户数据并使用 mongodb 储存；
3. 使用可视化工具 pyecharts, 对数据进行可视化处理；
4. 整理分析。
## 运行环境
* python3.7
* windows
* jupyter notebook
* mongodb
## 运行依赖包
* pymongo
* scrapy
* pyecharts
* jieba
* wordcloud
## 文件说明
### code 项目代码
* **zhihu** scrapy 项目代码文件，user_data.py 粉丝数 1w 以上用户信息抓取代码； article.py 粉丝数 10w 以上用户文章信息抓取；huida.py 粉丝数 10w 以上用户回答信息。
* **zhihu_plot.ipynb pyecharts** 图表绘制文件。
### zhihu_html 
* 里面包含可视化操作后的大部分文件；
* **zhihu_user.html** 主要为 pyecharts 绘制的粉丝数、点赞数、回答数等排行；
* **zhihu_p.html** 用户回答、文章随时间变化折线图；
* **zhihu.jpg** 粉丝数 1w 以上用户信息词云。
### node
* 粉丝数前50的高关注用户关系图；
* **node50.xlsx** gephi 所需的节点文件，文件中 id 列为粉丝数前50用户名, weight 列为粉丝数；
* **edge50.xlsx** gephi 所需的边文件，文件中 target 列为关注用户，source 列为被关注用户；
* **zhihu.gephi** 为生成的图文件，可直接用 gephi 打开，gephi 具体操作可见<https://github.com/spiderbeg/marvel-gephi>；
* **zhihu_module.png** 为以粉丝数为节点大小的用户关系图；
* **zhihu_连出度.png** 为以用户关注数为节点大小的用户关系图；
* **zhihu_连入度.png** 为以用户被关注数为节点大小的用户关系图。
## 一些建议及注意事项
## 建议
* 如何安装 git 见 <https://mp.weixin.qq.com/mp/appmsg/show?__biz=MjM5MDEyMDk4Mw==&appmsgid=10000361&itemidx=1&sign=f88b420f70c30c106697f54f00cf2a95>；
* MongoDB 安装：<http://mongoing.com/archives/25650> ；使用：<https://juejin.im/post/5addbd0e518825671f2f62ee>;
* gephi 具体操作可见<https://github.com/spiderbeg/marvel-gephi>；
* 不熟悉 scrapy 的瞧一眼这里：<https://cuiqingcai.com/3472.html>;
* scrapy 项目抓取代码中用到了 web 代理及多 cookie，需在填入自己的 web 代理及 cookie 值。就抓取时间 2019-7-23 来说不单用户单 IP 的抓取时间间隔为 0.45s, 具体时间与状况还需各位亲自尝试；
* pyecharts 绘制图形生成 html 文件，为方便本地查看可视化效果。把所需的 js 文件一并放置于此目录下；因此建议下载整个**zhihu_html文件夹**到本地后查看。
## scrapy 设置的简单介绍
* scrapy 的设置文件在 /zhihu_data/code/zhihu/settings.py 中，
 * ROBOTSTXT_OBEY = False 表示不遵守爬虫规则；
 * DOWNLOAD_DELAY = 0.15  表示下载延迟为0.15秒；
 * COOKIES_ENABLED = False 表示若需要cookie，则自己设置cookie。
## 如何跑起来
1. 确定好放置项目位置

         git clone https://github.com/spiderbeg/zhihu_data.git

2. 进入 /zhihu_data/code/zhihu/spiders 文件夹，打开 user_data.py, article.py, huida.py, 写入自己的代理，及cookie。打开控制台，进入 /zhihu_data/code/zhihu, 输入以下命令，即可抓取粉丝数 1w 以上用户回答数、点赞数、粉丝数等信息。 

         scrapy crawl user_data

3. 用户信息抓取完毕后，按照第二步所示命令，修改 user_data 为 article，为抓取粉丝数 10w 以上用户发布文章信息，huida 则为粉丝数 10w 以上用户回答的详细信息。
4. 找到 /zhihu_data/code/zhihu_plot.ipynb, 可直接将此文件放置于 jupyter notebook 文件夹下，修改生成图表文件路径即可。 
5. 部分代码
## 部分效果展示
* 粉丝数 1w 以上用户信息词云图
![publish](zhihu_html/zhihu.jpg)<br>
* 粉丝数前50用户关系图（节点大小代表粉丝数）
![publish](node/zhihu_module.png)<br>
