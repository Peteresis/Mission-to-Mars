# Mission to Mars

## :one: Objective
Create a web application that scrapes data from various websites and displays it in a single HTML page, using Flask, Bootsrap and Python.
 
## :two: Procedure

The procedure to create a Flask web application that displays scraped information in a new webpage has several steps.

### Step 1: Scrape the web sources and save the data into a dictionary

First, it is neccesary to develop the scraping code.  In our case, the scraping code was developed and tested in a Jupyter notebook (`Mission_to_Mars_Challenge.ipynb`) and then exported to a python file (`Mission_to_Mars_Challenge.py`). 

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

The process starts opening a Flask instance, and then using PyMongo to connect to the MongoDB server. The final part of the code creates the 'routes' that will be part of the Flask application.  

The `app.py` code is connected to the scraoer using the /scrape route. The data scraped is saved into a Mongo database using `upsert=True` to avoid duplicating or repeating scraped information to be saved into the database. This route's endpoint redirects to the home route. The home route searches the Mongo database for one data record and then renders the index.html template with that record.

The /scrape route was linked to a button in index.html, which a user could click to start the scrape.

### Step 3: Use an HTML file and Bootstrap to display the scrape results

The [HTML Code](https://github.com/Peteresis/Mission-to-Mars/blob/c048ea0372162cec77c6b0dd5cfe55d94ff0ec5e/index.html) is saved into a file called `index.html`, this file needs to be run in the first place, then the user needs to click the `Scrape New Data` button to begin the process of connecting to the `app.py` file which in turn connects to the `Mission_to_Mars_Challenge.py` file to do the scraping.  

So, even though we have described the process as `Mission_to_Mars_Challenge.py` ▶️ `app.py` ▶️ `index.html`, for a user the process occurs in reverse.  This is, `index.html` ▶️ `app.py` ▶️ `Mission_to_Mars_Challenge.py`.

#### Image 1: Process of creating a Flask App site
<img src="https://github.com/Peteresis/Mission-to-Mars/blob/2b4ac7f7776d76395e123f8ebcbb3e11eb4eafca/resources/data-10-5-3-1-flowchart.png" width=50% height=50%>


A brief description of what the HTML code does is as follows:

- There is a `<head>` section that displays the title of the page.
- There is a `<body>` section that includes the rest of the parts of the page, as follows:
- A `<div class="container">` that holds a `Jumbotron` header, part of the styles imported from Bootstrap.  This section also includes the `Scrape New Data` button.
- There is a section to present Mars News.
- There is another section to display the Featured Image and facts table.
- The code also includes a section for error handling.
- Finally, there is a section to show the images of the different hemisperes of mars and their title caption. 
 
## :three: Final Result.  A responsive webpage.

This is how the wepage looks in desktop mode
#### Image 2: HTML rendering in desktop mode
<img src="https://github.com/Peteresis/Mission-to-Mars/blob/13a8f2be5bdc0e1699ea8d2062ce9d7292c987cf/resources/Desktop.png" width=50% height=50%>

And this is how it looks in mobile mode.  This is a partial view because the page is too long to display completely here.
#### Image 3: HTML rendering in mobile mode
<img src="https://github.com/Peteresis/Mission-to-Mars/blob/13a8f2be5bdc0e1699ea8d2062ce9d7292c987cf/resources/Mobile.png" width=50% height=50%>

## References
**Module 10: Web Scraping to Extract Online Data**, https://courses.bootcampspot.com/courses/1145/pages/10-dot-0-1-web-scraping-to-extract-online-data, :copyright: 2020-2021 Trilogy Education Services, Web 15 Apr 2022.

**How To Use MongoDB in a Flask Application**, https://www.digitalocean.com/community/tutorials/how-to-use-mongodb-in-a-flask-application

**Integrating MongoDB with Flask Using Flask-PyMongo**, https://stackabuse.com/integrating-mongodb-with-flask-using-flask-pymongo/
