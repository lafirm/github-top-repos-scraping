# Github Top Repos Scraping
Scrape the Top 30 Repositories for each Topic on Github using BeautifulSoup and requests library.

![Github Image](https://preview.redd.it/g38817mqb1361.png?width=960&crop=smart&auto=webp&s=063b72aee824ef4f41cd58b3944b877d8a7f23e8)


## Introduction: 

In this project, we will scrape top 30 repositories for each topic on github page using `requests` and `BeautifulSoup` library.


### Project Outline:

- We have to scrape this paginated webpage: https://github.com/topics, to get the entire list of topics available on Github
- Use the `requests` library to download the page and `BeautifulSoup` library to parse and extract the information
- Create a dataframe for the list of Topics which should contain topic title, topic page URL, and topic description

- With the dataframe created, use the `requests` library to download the page for each topic using the topic page URL
- Now use the `BeautifulSoup` library to parse and extract the information from the downloaded topic pages
- Create a dataframe for each topic which should contain username, repo name, stars, and repo URL of top 30 repositories and it should be in the below format:

```
username,repo_name,stars,repo_url
mrdoob,three.js,83700,https://github.com/mrdoob/three.js
libgdx,libgdx,20200,https://github.com/libgdx/libgdx
```

#### Note:
1. To create a CSV file, prepare a dictionary of lists
2. Create a pandas dataframe from dictionary of lists using `pd.DataFrame()` method
3. Convert the dataframe into CSV file using `df.to_csv()` method



## Install and Import required libraries
      !pip install requests beautifulsoup4 pandas jovian --upgrade --quiet
      


## Scrape the list of Topics

### Download and Create Soup Doc

Let's define a helper function to download the topics list web pages which spans over 6 pages using `requests` library and parse the downloaded information using `BeautifulSoup` class from `bs4` library.


### Extract Topic Titles

Once the soup doc was created using the `soupify_topics_list_pages()`, we have to go through the webpage html to extract the required information like topic title, topic description and topic URL using the inspect elemets option which is available in browsers like `Google Chrome`, `Brave`, `Mozilla Firefox` etc.

![Topic Title Class Image](https://i.imgur.com/F8DWSTB.png)

`topic_title_class` was identified as `'f3 lh-condensed mb-0 mt-1 Link--primary'` using the inspect elements option available under developer tools.

Using the `topic_title_class`, we collected all the `<p> tags` which contains the topic title and the topic title was extracted using `text()` method.




### Extract Topic Descriptions

Similar to the process of extracting topic titles, topic descriptions were extracted after identifying `'f5 color-fg-muted mb-0 mt-1'` as `topic_desc_class`.



### Extract Topic URLs

URL for each topics were created by concatenating the base URL `"https://github.com"` with text available in `<a> tag` of class name `'no-underline flex-1 d-flex flex-column'`.


### Create Topics List Dataframe

Now we have 3 functions, each of which returns a list of topic title, topic description and topic URL. 

Let's define another helper function where these lists are gathered to create a dictionary which will be later converted into pandas dataframe.



## Scraping Top Repos for each Topic


Once topics list were scraped successfully, we have to scrape top 30 repositories (each topic page contains only 30 repos) for each topic page.

1. Download each topic page using topic URL from topic_df
2. Use the soup doc created by `soupify_topics_page()` to make a dataframe using `create_top_repos_df()`
3. Then create CSV file (if not exists) in `data` folder for each topic which contains top 30 repos



