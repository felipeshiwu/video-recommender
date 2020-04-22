# Video recommender

## What is it
This project was built from the one guided by the Data Science course [Como criar uma solução completa de Data Science | Mario Filho](http://mariofilho.com/curso/).

The objective of this project is to create a Youtube video recommender, following a certain criterion which will be used to list a series of videos that, according to a machine learning score, we consider recommended.

The data science process of this project is divided into 4 macro steps:
- Data Scraping
- Data Cleaning
- Labeling
- Modeling

### Tools
The development of the project used the following main tools:
- Core language: Python
  - Flask
  - Scikit Learn
    - Random Forest
    - Logistic Regression
  - LightGBM
  - BS4
  - Tf-IDF
  - Pandas and Numpy
  - joblib
- IDE: Jupyter Notebook
- The project is currently hosted on cloud: Heroku

## Data Scraping
As its name says, data science. So the first step is to collect the necessary and useful data for our proposal. What we do here is Web Scraping, a common strategy which gets the entire HTML page one by one and creates a csv file with the useful features gotten by the Youtube HTML tags. That is because we don't have a database ready to work, so web scraping was the solution found. For this project, the web scraping will be on youtube search page with keywords:
- Machine Learning
- Data Science
- Kaggle

## Data Cleaning
The point here is, when we get the entire HTML page, we also get a lot os useless information. To clean this data, what we use is BS4 to parse the HTML and search which tag/class have useful values for the main problem. In the end, what we choose to keep from all this information got are:
- Title
- Channel
- Description
- Publish date
- Views
- Resolution
- Video content tags

An important point here is that these fields above are not the features that we will use to labeling, only the information that we judge useful to maintain and from which the features for machine learning will be taken.

## Labeling
Getting here, what we have is a clean dataset and structured data with the relevant fields. Now what we need to do is select a part of that data and label it with **1 = I'm interested | 0 = I am not interested.**
To be more specific, 1600 videos were collected and I chose 500 videos to label. The criteria I used to classify as interesting video were:
- Videos lasting less than an hour 
- Titlies in English, Portuguese and Chinese
- Titles with **python** or **statistics** or **kaggle challenges**
- Titles with big technology company names
- Titles with fun facts
- Videos with more then 1500 views
- No lives
- No conference, except TED talk
- Videos with a reasonable image and audio resolution

The definition of the criteria depends a lot on the need and the objective of the project. In addition, well-defined labeling makes it easy to metrics validation.

After the first data labeling, we use the active learning strategy, which consists in using machine learning to search for a specific group of data that we call hard decisions so that I can manually classify and optimize the learning. In this project it uses the **Random Forest** to find the videos with probability between 0.45 and 0.55. And then I did the manual labeling for the second time.

Now is just split the data for test and validation and also convert title to [Tf-IDF](https://pt.wikipedia.org/wiki/Tf%E2%80%93idf).

## Modeling
We already realized that this problem is about classification, so the options are, among them: **Decision Tree**, **Random Forest**, **LightGBM**, **Logistic Regression** and **SVM**. After I tested each one, I decided to combine **Random Forest**, **LightGBM** and **Logistic Regression** with simple arithmetic mean. For **LightGBM** in particular, Bayesian Optimization was used to improve the parameters. Now we have trained models, and with that we can already predict the videos.

Of course in this project we did a little web app to display a list of videos with the best scores. The logic is simple, we do web scraping periodically and then we apply the trained models to get the scores. The displayed list is the list sort by score.

## About me
Autor - Felipe Shi Iu Wu | Contatos: [felipeshiwu@gmail.com] & [LinkedIn](https://www.linkedin.com/in/felipeshiwu/)
