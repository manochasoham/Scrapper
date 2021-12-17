# Scrapper
collected reviews under one roof. Used Web Scrapping teachnique  BeautifulSoap for the work.
#import libraries 
from bs4 import BeautifulSoup
import datetime
import requests
import pandas as pd

url="https://www.flipkart.com/apple-iphone-12-black-64-gb/p/itma2559422bf7c7?pid=MOBFWBYZU5FWK2VP&lid=LSTMOBFWBYZU5FWK2VPUYA8BN&marketplace=FLIPKART&q=iphone+12&store=tyy%2F4io&srno=s_1_1&otracker=AS_QueryStore_OrganicAutoSuggest_1_6_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_6_na_na_na&fm=SEARCH&iid=76d2c16f-7845-4717-b502-c26e491c736d.MOBFWBYZU5FWK2VP.SEARCH&ppt=hp&ppn=homepage&ssid=y96cn5wt680000001639683764104&qH=7b7504afcaf2e1ea"
data=requests.get(url)
soup=BeautifulSoup(data.content,"html.parser")
# print(soup)
# To prettify the html content

soup2=soup.prettify()
# print(soup2)

#print the name of customer in html

names=soup.findAll('p',class_="_2sc7ZR _2V5EHH")
# print(names)

# to create  list of customers 
cust_review_name=[]
for i in range(0,len(names)):
    cust_review_name.append(names[i].get_text())

# print(cust_review_name)

# print title review
review_title=soup.findAll('p',class_="_2-N8zT")
# print(review_title)

title=[]
for i in range(0,len(review_title)):
    title.append(review_title[i].get_text())
    
    
# print(title)

# finding how many stars customer give to the product
rate=soup.findAll('div',class_="_3LWZlK _1BLPMq")
# print(rate)

rating=[]
for i in range(0,len(rate)):
    rating.append(rate[i].get_text())

    
# print(rating)


review=soup.findAll('div',{"class":"t-ZTKy"})
# print(review)

reviews=[]
for i in range(0,len(review)):
    reviews.append(review[i].get_text())
    
# print(reviews)

# import pandas

# import pandas as pd
df=pd.DataFrame()
df['customer_name']=cust_review_name
df['customer_title']=title
df['customer_rating']=rating
df['customer_review']=reviews


# print(df)
# dump this data into excel file
df.to_excel(r"E:\reviews.xlsx",index=True)
