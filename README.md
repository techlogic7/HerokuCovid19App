# herokucovid19app

## Automate Web Scraping to Excel using Heroku

This code will allow you to scrape a page automatically, process it and email it to yourself using sendgrid based on a user defined schedule. This snippet of code will allow you to deploy your python script to Heroku and run a custom scheduler. This is meant for free accounts that do not have a credit card on file. Otherwise you would need to download add-ons but to do so you need a credit card on file. This code allows you to run a scheduler without a credit card on file.

# Step 1: Set Up Your Code
from selenium import webdriver \
import os

chrome_options = webdriver.ChromeOptions() \
chrome_options.binary_location = os.environ.get("GOOGLE_CHROME_BIN") \
chrome_options.add_argument("--headless") \
chrome_options.add_argument("--disable-dev-shm-usage") \
chrome_options.add_argument("--no-sandbox") \
driver = webdriver.Chrome(executable_path=os.environ.get("CHROMEDRIVER_PATH"), chrome_options=chrome_options)

# Now you can start using Selenium

# Step 2: Add the Buildpacks
On Heroku, open your App. Click on the Settings tab and scroll down to Buildpacks. Add the following:

1)Python (Select it from the officially supported buildpacks)
2)Headless Google Chrome: https://github.com/heroku/heroku-buildpack-google-chrome
3)Chromedriver: https://github.com/heroku/heroku-buildpack-chromedriver


# Step 3: Add the Config Vars
Scroll to the config vars section. Here, we will add the paths to Chrome and the Chromedriver. Add the following config vars:

CHROMEDRIVER_PATH = /app/.chromedriver/bin/chromedriver
GOOGLE_CHROME_BIN = /app/.apt/usr/bin/google-chrome


# Step 4: Deploy the Application
If everything worked out correctly, then your application should be ready to deploy!

# Deployment to Heroku Instructions (Heroku Git)
1) Sign up for a free heroku account if you havent already done so
2) Create app ie. myapp #name of app
3) Type heroku login --> This will take you to a web based login page
4) cd to your directory on your local drive
5) Type 'git init'
6) Type 'heroku git:remote -a myapp'
7) Type 'git add .'
8) Type ' git commit -am "version 1"'
9) Type 'git push heroku master'
10) Now you need to allocate a dyno to do the work. Type 'heroku ps:scale worker=1'
11) If you want to check the logs to make sure its working type 'heroku logs --tail'

Now your code will continue to run until you stop the dyno. To stop it scale it down using the command 'heroku ps:scale worker=0'
