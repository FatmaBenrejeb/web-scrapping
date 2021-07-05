# web-scrapping

from bs4 import BeautifulSoup
import requests

products=[] #List to store name of the product
#prices=[] #List to store price of the product
#ratings=[] #List to store rating of the product

page = requests.get("https://www.flipkart.com/laptops/a~buyback-guarantee-on-laptops-/pr?sid=6bo%2Cb5g&amp;amp;amp;amp;amp;amp;amp;amp;amp;uniq=")

soup = BeautifulSoup(page.content,'html.parser')

for a in soup.findAll('a',href=True, attrs={'class':'_1fQZEK'}):
    prod={}
    prod['name']=a.find('div', attrs={'class':'_4rR01T'}).text
    prod['price']=a.find('div',attrs={'class':'_30jeq3 _1_WHN1'}).text
    products.append(prod)

#print(products) #this shows {'product': , 'price': }
