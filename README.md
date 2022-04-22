# Mission to Mars

## :one: Objective
Create a web application that scrapes data from various websites and displays it in a single HTML page, using Flask, Bootsrap and Python.
 
## :two: Procedure

The procedure to create a Flask web application that displays scraped information in a new webpage has several steps.  First, it is neccesary to develop the scraping code.  In our case, the scraping code was developed and tested in a Jupyter notebook (`Mission_to_Mars_Challenge.ipynb`) and then exported to a python file (`Mission_to_Mars_Challenge.py`). 

The code connects to the `chromedriver` application which opens an instance of a browser window and navigates to the pages that are going to be scraped. The first page visited was [Mars Planet Science](https://redplanetscience.com/), a NASA Mars News website.  The scraper retrieved the most recent article's title and intro text (or lede).  The results were saved in variables with the aid of `BeautifulSoup`, an HTML parser application.

The following page visited was the [Space Images from Mars](https://spaceimages-mars.com), a site operated by the Jet Propulsion Laboratory.  The objective of visiting this site was to get the full-sized featured image of the day. The scraper clicked on the image button and parsed the html code of  the page to retrieve the image url.

It is worth noting that any scraping activity could throw errors if the elements of a page being scraped are not present because they have not had time to be loaded.  The internet speed connection can change because limitations of the internet connection being used, or the response time of the server, etc.  In order to avoid these errors it is advisable to add a line to our code that pauses for a few seconds before attempting to scrape any page.  This 'trick' avoids getting errors during code execution    and After visiting the first page, I needed to visit two more links, so I used browser.click link by partial text() and time.sleep() to avoid errors. I then used soup.find all() and. a[‘href'] to get the relative image path, which I combined with the main URL.



Third, I would grab the latest tweet from the Mars Weather Twitter Account. Like the first page, this was done by parsing the HTML to find the required element and then grabbing the text from it.



Then I scraped Mars facts from Space Facts. Rather than BeautifulSoup, I used Pandas to scrape the data. Pd.read html() scraped for tables and returned the second table with the data I needed. Renaming columns and setting indexes before converting df.to html ().



The USGS Astrogeology page also has images and names of all four hemispheres of Mars. I found the hemisphere titles using BeautifulSoup and saved them in a list called hemi names. Then I searched for all thumbnail links in the hemispheres and iterated through the results, checking if the thumbnail element contained an image. A list (thumbnail links) outside the loop was appended with the full image URL if true. To get the full-sized hemisphere images, I searched for all img elements with a wide-image class in thumbnail links. The results were used to retrieve the hemispheres' full image path, which was stored in full imgs. Iterated through the zipped object, appending the hemisphere title to an empty dictionary as a key and the image URL as the value, then appending that dictionary to an empty list.



It was then copied from the notebook to a Python file and used to create a scraping function. The scraping results were then stored as a dictionary and returned at the function's end.



### Image 1: Screenshot of the `measurement` table without any filters
<img src="https://github.com/Peteresis/Mission-to-Mars/blob/21b423b93bb124731b2d458dca3d4d55da9d589e/resources/data-10-5-3-1-flowchart.png" width=50% height=50%>








## References
**Module 10: Web Scraping to Extract Online Data**, https://courses.bootcampspot.com/courses/1145/pages/10-dot-0-1-web-scraping-to-extract-online-data, :copyright: 2020-2021 Trilogy Education Services, Web 15 Apr 2022.

**How To Use MongoDB in a Flask Application**, https://www.digitalocean.com/community/tutorials/how-to-use-mongodb-in-a-flask-application

**Integrating MongoDB with Flask Using Flask-PyMongo**, https://stackabuse.com/integrating-mongodb-with-flask-using-flask-pymongo/
