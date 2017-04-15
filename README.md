fish-percent-chart
===================

creative visualization 
-----------------

```r
library(tidyverse)
require(grid)
library("Rmisc")
```

```r
px1<-seq(from=0,to=10,length=1000)
py1<-sqrt(5^2-(px1-5)^2)

Project1x<-c(px1,rev(px1))
Project1y<-c(py1,-py1)
```

-------------------------------------------------------------------------------------


```r
Project1<-data.frame(lon=Project1x,lat=Project1y)
Project1$group<-"ProjectA"
Project1$order<-1:nrow(Project1)

Project2<-data.frame(lon=Project1x+15,lat=Project1y)
Project2$group<-"ProjectB"
Project2$order<-1:nrow(Project2)

Project3<-data.frame(lon=Project1x+30,lat=Project1y)
Project3$group<-"ProjectC"
Project3$order<-1:nrow(Project3)

Project4<-data.frame(lon=Project1x+45,lat=Project1y)
Project4$group<-"ProjectD"
Project4$order<-1:nrow(Project4)

Project5<-data.frame(lon=Project1x+60,lat=Project1y)
Project5$group<-"ProjectE"
Project5$order<-1:nrow(Project5)

Project<-rbind(Project1,Project2,Project3,Project4,Project5)
```

```r
ggplot(Project)+geom_path(aes(lon,lat,group=group))
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/one.png" width = "632.6" height = "130.8" alt="one" align=center />
</div>


----------------------------------------------------------------------

```r
Proj1<-Project1[,1:2]%>%filter(lat<=-4)
Proj1[nrow(Proj1)+1,]<-c(8,-4)
Proj1$group<-"ProjA"
Proj1$order<-1:nrow(Proj1)

Proj2<-Project2[,1:2]%>%filter(lat<=-3)
Proj2[nrow(Proj2)+1,]<-c(24,-3)
Proj2$group<-"ProjB"
Proj2$order<-1:nrow(Proj2)

Proj3<-Project3[,1:2]%>%filter(lat<=0)
Proj3[nrow(Proj3)+1,]<-c(40,0)
Proj3$group<-"ProjC"
Proj3$order<-1:nrow(Proj3)

Proj4<-Project4[,1:2]%>%filter(lat<=3)
Proj4$group<-"ProjD"
Proj4$order<-1:nrow(Proj4)

Proj5<-Project5[,1:2]%>%filter(lat<=4)
Proj5$group<-"ProjE"
Proj5$order<-1:nrow(Proj5)

Projdata<-rbind(Proj1,Proj2,Proj3,Proj4,Proj5)
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/two.png" width = "635.8" height = "135.5" alt="two" align=center />
</div>

---------------------------------------------------------------------------

```r
windowsFonts(myFont=windowsFont("msyh.ttc"))
labeldata<-data.frame(x=seq(from=5,to=65,length=5),y=c(-4,-3,0,3,4),label=sprintf("%2d%%",c(10,20,50,80,90)))
```

```r
p1<-ggplot()+
geom_polygon(data=Projdata,aes(x=lon,y=lat,group=group),fill="#92D24F",col=NA)+
geom_path(data=Project,aes(x=lon,y=lat,group=group),col="black",size=1.2)+
geom_text(data=labeldata,aes(x=x,y=y+1,label=label),hjust=.5)+
scale_x_continuous(breaks=labeldata$x,labels=paste0("Project",LETTERS[1:5]))+
ylim(-5.5,6)+
theme_minimal()+
theme(
panel.grid=element_blank(),
axis.title=element_blank(),
axis.text.y=element_blank(),
plot.margin = unit(c(.2,.2,1,.2), "cm")
)
```


<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/five.png" width = "635" height = "135" alt="five" align=center />
</div>



```r
p2<-ggplot()+
geom_polygon(data=Projdata,aes(x=lon,y=lat,group=group),fill="#FFC000",col=NA)+
geom_path(data=Project,aes(x=lon,y=lat,group=group),col="black",size=1.2)+
geom_text(data=labeldata,aes(x=x,y=y+1,label=label),hjust=.5)+
scale_x_continuous(breaks=labeldata$x,labels=paste0("Project",LETTERS[1:5]))+
ylim(-5.5,6)+
theme_minimal()+
theme(
panel.grid=element_blank(),
axis.title=element_blank(),
axis.text.y=element_blank(),
plot.margin = unit(c(.2,.2,1,.2), "cm")
)
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/six.png" width = "635" height = "135" alt="six" align=center />
</div>



```r
grid.newpage()
pushViewport(viewport(layout=grid.layout(2,2)))
vplayout <- function(x,y){viewport(layout.pos.row = x, layout.pos.col = y)}
print(p1,vp=vplayout(1,1:2))
print(p2,vp=vplayout(2,1:2))
```


<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/three.png" width = "681.6" height = "323.6" alt="three" align=center />
</div>



```r
library(gridExtra)
library("plyr")
library("lattice")
multiplot(p1,p2,layout=matrix(c(1,1,2,2),nrow=2,byrow=TRUE))
```

<div  align="center">    
<img src="https://github.com/ljtyduyu/fish-percent-chart/blob/master/Image/four.png" width = "700" height = "280" alt="four" align=center />
</div>

联系方式：
----------------------------------------------------
wechat：ljty1991  <br>
Mail:578708965@qq.com <br>
个人公众号：数据小魔方（datamofang） <br>
团队公众号：EasyCharts <br>
qq交流群：[魔方学院]553270834

个人简介：
-------------------------------------------------
**杜雨** <br>
财经专业研究僧； <br>
伪数据可视化达人； <br>
文科背景的编程小白； <br>
喜欢研究商务图表与地理信息数据可视化，爱倒腾PowerBI、SAP DashBoard、Tableau、R ggplot2、Think-cell chart等诸如此类的数据可视化软件，创建并运营微信公众号“数据小魔方”。 <br>
Mail:578708965@qq.com <br>
![resume](https://github.com/ljtyduyu/FontMap-of-China/blob/master/Image/resume.png)

-------------------------------------

友情推荐：
-------------------------------------------
**周闻文**：Python爬虫大神，各种炫酷高能手法玩出爬虫新境界！！！<br>
#### 简书主页：[duohappy](http://www.jianshu.com/u/5a8f3b911f56)



备注信息：
----------------------------------------------------
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">知识共享署名-非商业性使用 4.0 国际许可协议</a>进行许可。


