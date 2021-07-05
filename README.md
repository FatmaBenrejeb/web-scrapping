# web-scrapping

import pandas as pd
from bs4 import BeautifulSoup
import requests

product=[]
prices=[]
desc=[]
promo=[]
page = requests.get("https://www.animoes.tn/categorie-produit/boutique_chats/")

soup = BeautifulSoup(page.content,'html.parser')
#print(soup.prettify())
#print(soup.children)
for a in soup.findAll('a',href=True, attrs={'class':'_1fQZEK'}):
    name=a.find('div', attrs={'class':'_4rR01T'})
    description=a.find('div', attrs={'class':'fMghEO'})
    price=a.find('div', attrs={'class':'_3tbKJL'})
    promotion=a.find('div', attrs={'class':'_3Ay6Sb'})
    products.append(name.text)
    prices.append(price.text)
    desc.append(description.text)
    promo.append(promotion.text)
df = pd.DataFrame({'Product Name':product,'Descriptions':desc,'Price':prices,'Promotions':promo}) 
df.to_csv('products.csv', index=False, encoding='utf-8')
