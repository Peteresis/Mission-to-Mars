# Mission to Mars

## :one: Objective
Create a web application that scrapes data from various websites and displays it in a single HTML page, using Flask, Bootsrap and Python.
 
## :two: Procedure

### Step 1: Scrape the web sources and save the data into a dictionary

The procedure to create a Flask web application that displays scraped information in a new webpage has several steps.  First, it is neccesary to develop the scraping code.  In our case, the scraping code was developed and tested in a Jupyter notebook (`Mission_to_Mars_Challenge.ipynb`) and then exported to a python file (`Mission_to_Mars_Challenge.py`). 

The code connects to the `chromedriver` application which opens an instance of a browser window and navigates to the pages that are going to be scraped. The first page visited was [Mars Planet Science](https://redplanetscience.com/), a NASA Mars News website.  The scraper retrieved the most recent article's title and intro text (or lede).  The results were saved in variables with the aid of `BeautifulSoup`, an HTML parser application.

The following page visited was the [Space Images from Mars](https://spaceimages-mars.com), a site operated by the Jet Propulsion Laboratory.  The objective of visiting this site was to get the full-sized featured image of the day. The scraper clicked on the image button and parsed the html code of  the page to retrieve the image url.

:warning: It is worth noting that any scraping activity could throw errors if the elements of a page being scraped are not present because they have not had time to be loaded.  The internet speed can change because limitations of the internet connection being used, or the response time of the server, etc.  In order to avoid these errors it is advisable to add a line to our code that pauses for a few seconds before attempting to scrape any page.  This 'trick' avoids getting errors during code execution.  In the code written there are several lines that pause for 3 seconds before attemping to do the scrape.

The next step for the scraper was to visit the site [Mars Facts](https://galaxyfacts-mars.com/) to collect a table with general data about the red planet.  This table was later loaded into a pandas DataFrame that compares the information of Mars with that of the Earth.  Then the DataFrame was converted into HTML code using the `.to_html()` pandas function.

The final step in the scraping spree was to visit the [Planetary Data Science](https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars) of the US Geological Survey.  The intention of visiting this page was to collect the URLs of high resolution images of the different hemispheres of Mars and their titles.  This information was then added to a dictionary, as shown below:
```
[{'img_url': 'https://astropedia.astrogeology.usgs.gov/download/Mars/Viking/cerberus_enhanced.tif/full.jpg',
  'title': 'Cerberus Hemisphere Enhanced'},
 {'img_url': 'https://astropedia.astrogeology.usgs.gov/download/Mars/Viking/schiaparelli_enhanced.tif/full.jpg',
  'title': 'Schiaparelli Hemisphere Enhanced'},
 {'img_url': 'https://astropedia.astrogeology.usgs.gov/download/Mars/Viking/syrtis_major_enhanced.tif/full.jpg',
  'title': 'Syrtis Major Hemisphere Enhanced'},
 {'img_url': 'https://astropedia.astrogeology.usgs.gov/download/Mars/Viking/valles_marineris_enhanced.tif/full.jpg',
  'title': 'Valles Marineris Hemisphere Enhanced'}]
```
The code used to scrape the different sites mentioned can be found in the Git Hub repository [Mission-to-Mars/Mission_to_Mars_Challenge.py](https://github.com/Peteresis/Mission-to-Mars/blob/801af5ec29a5bcab93b0667887f35f6f331d8c89/Mission_to_Mars_Challenge.py) 

### Step 2: Use Flask to create a web application

Flask was used in a separate file, [app.py](https://github.com/Peteresis/Mission-to-Mars/blob/3d1354fe3ba6bbb626275bce9c3559cd342c49d8/app.py), to trigger the scrape function, update the Mongo database with the results, and then return that record of data from the database and onto a webpage.

The process starts opening a Flask instance, and then using PyMongo to connect to the MongoDB server. I used the /scrape route with this connection to run the scrape function from the imported scrape mars.py file. I then used update and upsert=True to update the Mongo database with the new collection from the scrape. This route's endpoint redirects to the home route. The home route searches the Mongo database for one data record and then renders the index.html template with that record.

The /scrape route was linked to a button in index.html, which a user could click to start the scrape. The remaining HTML file was formatted with Bootstrap to display the scrape results.







### Image 1: Screenshot of the `measurement` table without any filters
<img src="https://github.com/Peteresis/Mission-to-Mars/blob/21b423b93bb124731b2d458dca3d4d55da9d589e/resources/data-10-5-3-1-flowchart.png" width=50% height=50%>








## References
**Module 10: Web Scraping to Extract Online Data**, https://courses.bootcampspot.com/courses/1145/pages/10-dot-0-1-web-scraping-to-extract-online-data, :copyright: 2020-2021 Trilogy Education Services, Web 15 Apr 2022.

**How To Use MongoDB in a Flask Application**, https://www.digitalocean.com/community/tutorials/how-to-use-mongodb-in-a-flask-application

**Integrating MongoDB with Flask Using Flask-PyMongo**, https://stackabuse.com/integrating-mongodb-with-flask-using-flask-pymongo/
