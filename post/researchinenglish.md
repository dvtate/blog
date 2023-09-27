# Research in English
> 2023.8.1

[Research in English](https://researchinenglish.com) is a website I threw together over the course of a couple months. The website uses AI to read research papers and write news articles about them that are readable to the general public. The idea came to me after I was researching niche topics and managed to find a publication which was writing about research which was exactly what I was looking for but they didn't have any of the numbers or any other relevant information that I needed and didn't cite their sources or anything else. Further I read many other articles where the author neither read nor understood the paper that they were writing about. With these problems in mind I created Research in English.

I'm admittedly not a huge fan of AI-generated articles taking up all of the search results on the internet but in this case I genuinely think that it's providing value as the articles are definitely more readable. Each article is fairly cheap to generate and the papers are all provided under permissive licenses through various preprint services. Using preprints does open up the result of limited accuracy but I have noticed that most papers that eventually get shot down in review do eventually get withdrawn from the preprint services. So by writing about slightly dated papers (ie - 1 month delay) we significantly reduce the already small quantity of inaccuracies.

## How it Works
Here is a simplified overview of how an article comes to be. (note to self - TODO add pictures)

### Finding Papers
We use a number of sources for finding research papers to write about. We of course have to filter out the ones which don't have permissive licenses. We then categorize them, collect additional metadata, add them into our database.

### Reading Papers
Because PDF is not particularly conducive to automated reading systems (ie - columns can be read a number of different ways), we have a manual phase where a human does the following:
- look at the paper
- decide if it's newsworthy or not
- copy and paste sections from the paper (usually just a few fields)

### Writing Articles
After we the paper in an AI friendly format we use OpenAI's API to generate the article, headline, description, etc.

### Manual Review
The final step before the article is published is that a human can skim it and choose a relevant thumbnail.

### Static site generation
Finally, the articles in the database are converted into a complete static html website.

---------
You can also find this post [here](https://dev.to/dvtt/research-in-english-39ff)