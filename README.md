# python
  1.图片爬虫
  
# -*- coding: utf-8 -*-
# author liya

import re
import os
import urllib

url = "http://www.17sucai.com/preview/321248/2016-08-07/%E8%A1%A8%E7%99%BD/index.html"
imgcontent = urllib.urlopen(url).read()  # 抓取网页内容
urllist = re.findall("<img src='(.*?)' ",imgcontent)  # 提取图片链接
if not urllist:
    print 'not found...'
else:
    # 下载图片,保存在当前目录的pythonimg文件夹下
    filepath = os.getcwd() + '\pythonimg'
    if os.path.exists(filepath) is False:
        os.mkdir(filepath)
    x = 1
    print u'爬虫准备就绪...'
    for imgurl in urllist:
        imgurl_1 = "http://www.17sucai.com/preview/321248/2016-08-07/表白/" + imgurl
        temp = filepath + '\%s.jpg' % imgurl[4:-4]
        print u'正在下载第%s张图片' % x
        print temp
        print imgurl_1
        urllib.urlretrieve(imgurl_1, temp)
        x += 1
    print u'图片下载完毕，保存路径为' + filepath
