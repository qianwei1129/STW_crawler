import requests
import re
from lxml import html
from bs4 import BeautifulSoup
from urllib.request import  urlretrieve

# 1. 获取网页源码并转换成文本格式
def getcon():
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) '
                             'AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36'}
    url = "http://www.cnkang.com/cm/zcy/jry/"  # 中华康网上清热药的网址
    res = requests.get(url, headers=headers)  # 使用requests.get()函数访问该网址
    res.encoding = 'utf-8'  # 使用'utf-8'的编码格式来重新编码及解码
    res = res.text
    analyse(res)

# 2. 解析网页源码
def analyse(res):
    soup = BeautifulSoup(res, 'html.parser')
    med = soup.select('.catalog04  dd a')
    # 观察源码中带有每种植物与对应网址的在class为catalog04下，<dd>中的<a>标签
    med_name = []
    med_url = []
    # 创建两个存放名称和网址的列表
    for i in range(len(med)):
        temp = ('http://www.cnkang.com/' + str(med[i]['href']))
        med_name.append(med[i].text)
        med_url.append(temp.replace(" ", ""))
        # 将对应的名称和网址加入对应的列表中
    detailed_information(med_name, med_url)

# 3. 爬取各味清热药的别名，药性等信息
def detailed_information(name, url):
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) '
                             'AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36'}
    Introduction = [] # 用来存储简介
    medicinal = [] # 用来存储药性
    efficacy = [] # 用来存储功效与作用
    indications = [] # 用来存储适应症
    for i in range(len(url)):
        temp_url = url[i]
        temp_res = requests.get(temp_url)
        crawler(temp_res)

# 附3. 用来在源码中爬取具体信息
def crawler(res):
    tree = html.etree.HTML(res.content, html.etree.HTMLParser(encoding = 'utf-8'))
    temp_re = tree.xpath('//div[@class = "zh05b"]//p/text()')
    print(temp_re)

if __name__ == "__main__":
    getcon()


