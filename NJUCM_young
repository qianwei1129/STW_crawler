import requests
import time
import re
from bs4 import BeautifulSoup
from selenium import webdriver
from selenium.webdriver.common.by import By
from lxml import html

def getcon():
    global article_url
    browser = webdriver.Chrome()
    browser.get('https://weixin.sogou.com/weixin?query=南中医药院学子') # 访问南中医药院学子的官方公众号
    browser.find_element(By.XPATH, '//*[@id="query"]').clear() # 清除搜索框中原有的内容
    browser.find_element(By.XPATH, '//*[@id="query"]').send_keys('南中医药院学子') # 向搜索框中输入“南中医药院学子”
    browser.find_element(By.XPATH, '//*[@id="scroll-header"]/form/div/input[1]').click() # 点击搜索文章公众号
    time.sleep(3)
    for i in range(10):
        chrome_options = webdriver.ChromeOptions()
        chrome_options.add_argument('--headless')
        browser = webdriver.Chrome(options=chrome_options)
        shared_url = 'https://weixin.sogou.com/weixin?query=南中医药院学子&_sug_type_=&amp;sut=3242&amp;lkt=1%2C1644729398114%2C1644729398114&amp;s_from=input&amp;_sug_=n&amp;type=2&amp;sst0=1644729398216&amp;page=' + str(i + 1) + '&amp;ie=utf8&amp;w=01019900&amp;dr=1'
        browser.get(shared_url) # 获取公众号文章界面的源码
        data = browser.page_source
        analysis(data)
    article_url = article_url[0::2]  # 我发现每篇文章都会读取公众号的地址，因此提取奇数项
    print(article_url)

def analysis(res):
    global article_url
    soup = BeautifulSoup(res, 'html.parser')
    temp_url = soup.select('.txt-box a') # 观察源码中每篇文章网址在class为txt-box下，a标签
    for i in range(len(temp_url)):
        temp = ('https://weixin.sogou.com/' + str(temp_url[i]['href'])) # 在链接前补充我们需要的网址前缀
        article_url.append(temp)

if __name__ == "__main__":
    global article_url # 定义一个存放每篇文章网址的全局变量
    article_url = []
    getcon()
