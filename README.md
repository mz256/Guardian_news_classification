# News article classification by topic

## Summary
A text classifier is trained on a custom-built NLP dataset of news articles from the Guardian. The model is then deployed for inference as a web application with Dash. 

The script `scrape_guardian` uses the Guardian Open Platform API and BeautifulSoup to scrape and parse news articles about Hong Kong from January 1st 2018. These are then organised and saved as a dataset for analysis.