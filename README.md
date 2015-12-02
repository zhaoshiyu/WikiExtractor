# WikiExtractor 维基百科离线语料获取
## 一、介绍
意大利人用python写的维基百科离线语料抽取工具[WikiExtractor](http://medialab.di.unipi.it/wiki/Wikipedia_Extractor)；这里加了去掉几个特殊字符。

## 二、使用方法
### 1、维基百科语料获取
从
https://dumps.wikimedia.org/zhwiki/ ;
https://dumps.wikimedia.org/enwiki/ ;
https://dumps.wikimedia.org/thwiki/ 
下载不同语种的离线语料。
如下载中文语料:
```shell
wget https://dumps.wikimedia.org/zhwiki/20151123/zhwiki-20151123-pages-articles-multistream.xml.bz2
```
这个压缩包里面存的是标题、正文部分，如果需要其他数据，如页面跳转、历史编辑记录等，可以到目录下找别的下载链接。

### 2、使用 WikiExtractor 抽取正文文本
下载完成后使用下列命令抽取：
```shell
bzcat zhwiki-20151123-pages-articles-multistream.xml.bz2 | python WikiExtractor-zsy.py -b200M -o extracted > vocabulary.txt
```
参数 -b200M 表示以200M为单位切分文件，默认是 500K。

### 3、繁简转换
如果抽取中文的话需要将繁体转化为简体(维基百科的中文数据是繁简混杂的，里面包含大陆简体、台湾繁体、港澳繁体等多种不同的数据)。可以使用opencc进行转换，也可以使用其它繁简转换工具。

若使用opencc，ubuntu系统使用下列命令安装：
```shell
sudo apt-get install opencc
```
或者查看[这里](https://code.google.com/p/opencc/wiki/Install)
安装完成后使用下列命令转换：
```shell
opencc -i wiki_00 -o wiki_00_chs -c zht2zhs.ini
```
