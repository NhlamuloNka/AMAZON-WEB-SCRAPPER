# AMAZON-WEB-SCRAPPER
project to scrape the  prices

import requests
from bs4 import BeautifulSoup
import smtplib

URL='https://www.amazon.com/Sony-Full-Frame-Mirrorless-Interchangeable-Lens-ILCE7M3/dp/B07B43WPVK/ref=sr_1_1?dchild=1&keywords=sony+a7iii&qid=1591556165&sr=8-1'

headers= {"user-agent" :' Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.97 Safari/537.36 '}


def check_price():
    page = requests.get(URL,headers = headers)

    soup = BeautifulSoup(page.content, 'html.parser')

    title = soup.find(id = "productTile").get_text()
    price = soup.find(id="priceblock_ourprice").get_text()
    converted_price = float(price[0:5])

    if(converted_price<1.700):
        send_mail()

    print(converted_price)
    print(title.strip())

    if(converted_price < 1.700):
        send_email()

    def send_email():
        server = smtplib.SMTP('smtp.gmail.com',587)
        server.ehlo()
        server.starttls()
        server.ehlo()

        server.login('nhlamulo.proj@gmail.com', 'aufhxxrtjjhvkytn' )

        subject = 'Price fell down'
        body= check the amazon link 'https://www.amazon.com/Sony-Full-Frame-Mirrorless-Interchangeable-Lens-ILCE7M3/dp/B07B43WPVK/ref=sr_1_1?dchild=1&keywords=sony+a7iii&qid=1591556165&sr=8-1'

        msg = f"Subject: {subject}\n\n{body}"

        server.sendmail('nhlamulo.proj@gmail.com',msg)

        print('HEY EMAIL HAS BEEN SENT')

        server.quit()

        check_price()A
