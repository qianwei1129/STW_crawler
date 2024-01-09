import os
import xlrd
import requests

def Excel_read():
    '''定义读取excel的函数'''
    TCM_213 = xlrd.open_workbook(r'表单标题(1).xls' )
    sheet = TCM_213.sheet_by_name('Sheet0')
    Name = [] # 保存姓名
    Health_code = [] # 保存健康码
    Travel_card = [] # 保存行程卡
    NAT = [] # 保存核酸检测报告
    for a in range(sheet.nrows):
        cells = sheet.row_values(a) # 每行数据赋值给cells
        Name.append(cells[0])
        Health_code.append(cells[1])
        Travel_card.append(cells[2])
        NAT.append(cells[3])
    return(Name, Health_code, Travel_card, NAT)

def Download_picture(Name, Health_code, Travel_card, NAT):
    '''定义通过网址下载图片的函数'''
    for i in range(len(Name)):
        path = 'D:\威\中药213'
        temp_name = Name[i]
        os.makedirs(path + '\\' + temp_name)

        pic_Heath_code = (requests.get(Health_code[i])).content
        pic_Travel_card = (requests.get(Travel_card[i])).content
        pic_NAT = (requests.get(NAT[i])).content

        save_path = str("D:\威\中药213" + "\\" + temp_name)
        try:
            with open(save_path + str('\\健康码.jpg'), 'wb') as jpg:
                jpg.write(pic_Heath_code)
            with open(save_path + str('\\行程卡.jpg'), 'wb') as jpg:
                jpg.write(pic_Travel_card)
            with open(save_path + str('\\核酸检测.jpg'), 'wb') as jpg:
                jpg.write(pic_NAT)
        finally:
            jpg.close()

(Name, Health_code, Travel_card, NAT) = Excel_read()
Download_picture(Name, Health_code, Travel_card, NAT)
