# Flag Pieces - Project 4

## Contents

- [Contents](#contents)
- [Brief](#brief)
- [Approach](#approach)
- [Technologies Used](#technologies-used)
- [Wireframe](#wireframe)
- [Responsibilities and Code Review](#responsibilities-and-code-review)
  - [API Data](#api-data)
  - [Home Page](#home-page)
  - [Country Articles Page](#country-articles-page)
  - [Feed page](#feed-page)
  - [Single Article Page](#single-article-page)
  - [Reactions Backend Code](#reactions-backend-code)
- [Challenges and Key Learnings](#challenges-and-key-learnings)
- [Conclusions](#conclusions)

## Brief

Build a full-stack application by making your own backend and your own front-end. Use a Python Flask API using a Flask REST Framework to serve your data from a Postgres database. Consume your API with a separate front-end built with React. Be a complete product which most likely means multiple relationships and CRUD functionality for at least a couple of models. Implement thoughtful user stories/wireframes that are significant enough to help you know which features are core MVP and which can be left out.

## Approach

We decided on using News API as the main source of data for our application. We appreciated the way that the API was continuously updated so we could provide recent information for the user. We wanted to add our own unique features to the data by adding further fields such as flag images and user reactions. This would allow for a more interactive application and foster a distinctive appeal. Our aim was to make the application as open as possible therefore, user login pages are on selected pages only and accessibility and usability is prioritized.

## Technologies Used

- HTML; CSS/Sass; JavaScript; React
- PostgreSQL; Python; Flask; Flask SQLAlchemy
- Marshmallow; React Router; Node.js; Axios
- Bcrypt; Json Web Token; Mapbox
- Moment; Bulma


## Wireframe

For the purpose of planning our user journey, feature connectivity and points of access to data we constructed a wireframe that outlined the web application.
![UX Wireframe](./Flag%20Pieces%20Wireframe.png)

- [View Wireframe (figma.com)](https://www.figma.com/file/4Q0PFrOh3O7B23JmRmqdVw/PROJECT-R?node-id=0%3A1)

## Responsibilities and Code Review

Throughout this project we worked in collaboration (Raquel Cruickshank and I) and both appreciated each others opinion and perspective on project outcomes. Naturally, we also gravitated towards particular features that we wanted to implement, hence we also each worked confidently, independently on several occasions.

### API Data

We received data in json format from News API. We opted to pursue the strategy of storing the data into our backend database after the user interacted with the application by selecting to read an article. An advantage of this approach was that filtering of the data could be applied before storage in our backend. For example, we had the opportunity to delete some non essential keys from an API object before storing the information in the backend. Also quality control of the data could be applied to ensure a consistent and predictable user experience.

### Home Page

• For the homepage  I used Mapbox API to implement an interactive map.
• The country map data, including the latitude and longitude, was saved as an array of objects on the frontend.
• On click, the users selects a country to activate a popup. 
• Within the popup is the country name, flag and a link to the next page. 
• The country name is stored in the URL as a variable; the information can then be passed to the next page (country articles page). There the country
  variable would be set to the same value (e.g. const country = props.match.params.country)
  
Link - [Referenced Code](https://github.com/RichardBekoe/Flag-Pieces/blob/master/frontend/src/components/HomePage.js)

### Country Articles Page

• The code for the country articles page involves translating the country name from the URL (variable)
• There is a search in the dictionary (countryEmojiMap) of country name and flags.
• Therefore, a country is assigned a flag image.
• This information is saved in the backend, using the article model
• The page then changes to the 'singlearticle' page 
• The ID of article which is saved in the database is retrieved, therefore the user is redirected to that specific page with the selected article

Link - [Referenced Code](https://github.com/RichardBekoe/Flag-Pieces/blob/master/frontend/src/components/CountryArticles.js)

### Feed Page


• On the feed page we aimed to filter the articles by the reaction type i.e. 😂 😊 😲 😓 😠
• To do this we use the useEffect hook to get all the articles upon mounting the page.
• We used the filter method to filter through all the articles. We then mapped through the array of reactions. 
• A selection of articles of a particular reaction type,  would then be displayed on the page.
• This functionality provides the user a way to dynamically filter content based on users rated sentiment.
• However, as we carried out the filter through all the articles in the database, this method may not scale or be very efficient when the database is very large
• An alternate for this could be to redesign our backend to create models which categorise the articles by reaction type.

Link - [Referenced Code](https://github.com/RichardBekoe/Flag-Pieces/blob/master/frontend/src/components/FeedPage.js)

### Single Article Page


• We get the article with the same ID as the news item that was clicked on the previous page. And the content of the article is displayed on the page.
• This requires that the user is logged in.
• We had implemented, JWT and secure routes for entrance into certain areas of the website.
• When a user clicks a reaction image, a reaction object of the reaction type is made and the state of reaction is updated (useSatate).
• When the state of reaction changes a useEffect is called, which post the reaction to the backend reaction model.
• We also implement a useState where the colour of the button is conditional on whether it has been clicked.
• There is a test input box where users can type comments to each individual article, a handleComment function, performs an axios.post to the backend.

Link - [Referenced Code](https://github.com/RichardBekoe/Flag-Pieces/blob/master/frontend/src/components/SingleArticle.js)

### Reactions Backend Code

• The relationship between the reactions and the articles could be described as many-to-many (i.e. reactions = db.relationship( "Reaction", secondary=articles_reactions, backref="articles")
• We had to implement the modification of the reactions array for each article in the join table
• The method of adding a reaction to an article involved:
	○ posting a reaction to the backend
	○ loading new reaction to schema
	○ finding article by ID
	○ saving new reaction
	○ joining article with new reactions  (i.e. existing_article.reactions = existing_article.reactions + [new_reaction] )
	○ article.save()

• In the backend the base.py model allows methods such as, save and remove to be available for controllers to use. It also provides the 'created and updated at' times. 


Link - [Referenced Code](https://github.com/RichardBekoe/Flag-Pieces/blob/master/backend/models/article.py)

## Challenges and Key Learnings

The importance of planning, reviewing and revising code structure was a key learning point. For example, we initially had additional backend models but did not use them. Instead we joined the information as fields on other existing models. Alternatively, we also stored the information on the frontend of the application (e.g. the maps data).

However, with a large dataset this may not be a feasible option, as it may slow the loading of the application for the user. A different solution could have been to pre-seed the information for the maps using an available online database as a source. 

In addition, we envisioned further functionalities such as backend controllers so that people could save articles to their user page, which they had filtered by reaction. We used JWT and local storage to set user tokens and indicate when users are logged in. This allows the access of pages based on whether a user was logged in. To improve the user experience we could further suggest or prompt at what points they would need to be logged to access particular information. These are skills that we can build on in the future.


## Conclusions

Overall, I am very pleased with the outcome of our project work, of which was completed to fixed time constraints. I am appreciative of the team's determination to achieve a high standard. I am pleased with how we crafted the initial data we received and added and removed fields from the original information, for example, country flags and reaction images to tailor the needs of our application.
	
I enjoyed how we could architect the frontend interaction with the backend, and thought deeply about what information should be accessible where and when.
