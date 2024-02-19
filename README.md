# SNL Dream Team

This project started when I came across this (dataset)[https://github.com/hhllcks/snldb].

As a fan of SNL, this was a treasure trove. I constantly see debates online about the best SNL era, so I wondered if I could test that with this dataset. I also wondered, if there was a "all-start" SNL cast, who would it comprise of.

The learning goal I had for this project was to learn a new visualisation package I'm less familiar with.

## Data Gathering
I ran into troubles immediately when using the dataset. It relied on scrapy to scrape the data from (SNLArchives)[http://www.snlarchives.net/]. I had not prior experience with the library, so it was difficult to debug what exactly was going wrong. I tried to reach out to the authors of the library but they did not respond.

Eventually, with some external help, I realised that SNLArchives had probably gone through an update since the scraper was written, and the CSS references that scrapy was using was no longer correct. 

I considered rewriting the scraper in beautifulsoup or playwright, which on hindsight might have been a worthy attempt. But the trouble I had there was designing the database, especially given the time constraints I had for this project. In the end, I decided to just use the pre-scraped data from the repository, which had data all the way until 2021.

However, I still had to scrape IMDB for the episode ratings. This was relatively straightforward, and the process can be seen in the `new-scraper-test.ipynb`.

## Analysis
The analysis was the fun part. 

My immediate finding surprised me — that season ratings don't actually vary that much. 

I then had to figure out how to best rate cast members, given that the only evaluation I had were episode ratings. 

I first decided to exclude guests and musical hosts to make the analysis simpler. Then, I decided that I could give each cast member a weight based on the number of sketches they appeared in the episode.

I assigned each cast member a weighted score for the episodes they appeared in and ranked them by the average of all their scores. 

# Visualisation
I started out wanting to learn `layercake`, a visualisation package built in Svelte. Since my portfolio was in Svelte, I though this would be useful as an extension.

However, as I started looking into the documentation, I felt that I didn't have the basic fundamental concepts yet, and not enough time to properly pick it up. I decided to pivot to ggplot instead. 

ggplot is a package that we've alread learnt in class, but because it was gone through pretty quickly, I thought it was worthwhile to sit with it for a while, given its capabilities.

I also wanted a clean and reader facing way to present the rankings of _all_ the cast members. I plot it in my own exploratory analysis, but it was definitely way too big to be friendly for a reader on the web page. 

I thought then a small interactive component would be a good middle-ground. I already understand some Javascript basics, so I knew it was possible to build a small search component with vanilla HTML, CSS, and JS, and asked ChatGPT for help with it.

I then had trouble importing the json into the javascript file, so I relied on simply loading the data upfront within the `script.js`, given that it was only about 150 entries.

# Reflections
I think my methodology is not fullproof. One could question if it was the fairest way to evalauate cast members given that SNL is quite collaborative. Did a cast member actually contribute more to the episode just because they appeared more in it?

The other think that I couldn't account for is the host and the musical guest. Hosts definitely have a role to play in the ratings, so it would have been useful to come up with a metric to control for that as well.

I also wish I had a bit more time to explore how to translate a ggplot svg into an interactive graph. I do feel that the graph as a PNG makes the story feel a bit less alive than if I had just used datawrapper. But I understand that svg to html is a class in the near future, so I might update this story when I get there. 
