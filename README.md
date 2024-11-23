# revoberliana-web-scraping-assignment
Assignment web -scrapping using selenium

web source = https://www.gutenberg.org/ebooks/search/?sort_order=downloads&start_index=26
using selenium 
tujuan = untuk dapat mendapatkan data raw dari web books yang berisikan (title, subtitle dan extra)

proses = 
instalasi selenium
**!pip install selenium**

instalasi chrome browser,driver di goole collab
**!apt-get install -y chromium-browser**

**!apt-get update**

**!apt install chromium-chromedriver**

import modul selenium
**from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By**
define web driver
**def web_driver():
  options = webdriver.ChromeOptions()
  options.add_argument("--verbose")
  options.add_argument('--no-sandbox')
  options.add_argument('--headless')
  options.add_argument('--disable-gpu')
  options.add_argument('--disable-dve-shm-uage')
  driver = webdriver.Chrome(options=options)
  return driver**
  **driver = web_driver()**

get the web with driver 
**driver.get('https://www.gutenberg.org/ebooks/search/?sort_order=downloads')**

find element class
**books = driver.find_elements(By.XPATH, '//li[@class="booklink"]')**

find element title,subtitile,extra with looping for
**for container in books:
  title = container.find_element(By.XPATH, './/span[@class="title"]').text
  subtitle = container.find_element(By.XPATH, './/span[@class="subtitle"]').text
  extra = container.find_element(By.XPATH, './/span[@class="extra"]').text
  print(title, subtitle, extra)**

extra to goggle sheet 
**!pip install gspread**
**from google.colab import auth
auth.authenticate_user()
from google.auth import default
import gspread
creds, _ = default()
gc = gspread.authorize(creds)
gs = gc.create('scraped_books')
sh = gs.sheet1**

add data 
**sh.append_row(['title', 'subtitle', 'extra'])**
**sh.append_row([title, subtitle, extra])**

  
link the result : https://docs.google.com/spreadsheets/d/1aIDo5X8DBZyHH9hS075A_4L5KOWJZmQiznFYZzJclV0/edit?usp=sharing
