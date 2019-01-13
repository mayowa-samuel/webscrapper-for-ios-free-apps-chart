# webscrapper-for-ios-free-apps-chart
# a .py code to scrape, app serial number; app name; and app type, as in the url and save in a filename *.csv

from bs4 import BeautifulSoup as soup
from urllib.request import urlopen as uReq

my_url = 'https://www.apple.com/itunes/charts/free-apps/'

uClient = uReq(my_url)
page_html =uClient.read()
uClient.close()
page_soup = soup(page_html, "html.parser")

containers = page_soup.findAll("div", {"class":"section-content" })
# print(len(containers))
# print(soup.prettify(containers[1]))

container=containers[1]


# print(container.strong.text)
# print (container.h3.text)
# print (container.h4.text)


filename = "apple_itunes_charts_free_app.csv"
f = open(filename, "w", encoding="utf-8")

headers = "Serial_number,App_name,App_type \n"
f.write(headers)

for container in containers:

   Serial_number = container.strong.text

   App_name = container.h3.text

   App_type = container.h4.text


   print(Serial_number.replace(".", "") + "," + App_name + "," + App_type + "\n" )


   f.write(App_name_and_no.replace(",", "_").replace("    ", ",", 1) + "," + App_company.replace(",", "_") + "\n")
f.close()
