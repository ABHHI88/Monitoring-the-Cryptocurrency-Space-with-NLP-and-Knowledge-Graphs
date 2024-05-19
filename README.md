# Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs
Built a robust data pipeline using NLP and knowledge graphs for cryptocurrency analysis. Extracted insights, identified trends, and empowered decision-makers with predictive analytics, showcasing expertise in dynamic markets.

imagine you want to stay updated with all the latest information and insights in a particular field, but there's just too much to read. Well, there's a solution that combines two powerful technologies: Natural Language Processing (NLP) and knowledge graphs.

NLP helps computers understand human language, and knowledge graphs organize information in a meaningful way, like connecting the dots between different concepts.

By using a tool like Diffbot, which scours the internet to gather information and analyze it, you can automatically extract key insights from articles. This saves you tons of time and effort because you don't have to read everything yourself.

Think of it like this: You can set up a system that continuously monitors news articles about your company, competitors, or any topic you're interested in. It can even help investors by analyzing news about potential investments in stocks or cryptocurrencies.

Diffbot's Natural Language Processing API does the heavy lifting by figuring out what the articles are about and extracting important details. Then, you can store all this information in a graph database like Neo4j, which makes it easy to see connections between different pieces of information.

So, instead of spending months building your own system, you can use tools like Diffbot to get up and running in just hours. It's like having a super-smart assistant that sifts through the internet for you, so you can focus on making smarter decisions based on the insights it provides.

AGENDA
1. Find Cryptocurrency Articles: Search for articles that discuss cryptocurrency topics.
2. Translate Foreign Articles: If there are articles in languages other than your preferred one, use the Google Translate API to convert them.
3. Bring Articles into Neo4j: Import the articles into Neo4j, a type of database.
4. Extract Important Information: Use Diffbot's NLP API to identify key entities and facts within the articles.
5. Store Information in Neo4j: Save the extracted entities and facts into Neo4j.
6. Analyze the Graph: Use Neo4j to study the relationships between different entities and facts.
This process helps in efficiently gathering and analyzing information about cyptocurrency from various sources.

1. FINDING CRYPTOCURRENCY ARTICLES:
   We're going to use Diffbot's APIs to get articles discussing cryptocurrencies. If you want to try this yourself, sign up for a free trial on their website. Once you're logged in, you can use their visual query builder to see what's available. This code will fetch up to 5000 recent articles tagged with "cryptocurrency". It does this in batches of 50 articles each to make it more efficient. This way, you can gather a lot of useful data for analysis or whatever you need.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/4f60f590-ee1b-4695-a56a-4a82914b36ad)

There is a lot of data available by Diffbot’s Knowledge Graph API. So not only can you search for various articles, but you could use their KG APIs to retrieve information around organizations, products, persons, jobs, and more.

This example will retrieve the latest 5000 articles with a tag label Cryptocurrency.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/fa4b93f9-f9b9-4a4d-8b89-340b388a57d7)

2. TRANSLATE THE FOREGIN ARTICLES:
   The articles we got are from all over the world and in different languages. Next, we'll use the Google Translate API to translate them into English. To do this, you'll need to activate the Google Translate API and generate an API key.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/f09cecc5-8e26-4341-aaf7-2df61a6eb472)


3. BRING/IMPORT ARTICLES INTO Neo4j:
    I recommend either downloading Neo4j Desktop or using the free Neo4j AuraDB cloud instance. This will help us store information about the 5000 articles. First, we need to set up the connection to the Neo4j instance.
 
   ![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/34432f1b-3b87-40c4-a173-ae66e67ecf57)
   
The imported graph model will have the following schema.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/f1b7328d-0165-4082-859a-5ec315d4cea7)

We have some extra information about the articles. For instance, we know the general feeling of the article and when it was published. Also, for many articles, we know the author and the website it's from. Additionally, the Diffbot API provides categories for each article.

Before we move forward, we'll set up unique rules in Neo4j. This will help speed up the import process and make future searches faster.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/42a45500-cc5e-454e-ba8a-a68989175367)

Now we can go ahead and import articles into Neo4j.

vbvgte![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/bb439b17-db83-4a2e-95b8-7b2a1e509915)

I won't explain the above Cypher query in detail here. Instead, you can find multiple blog posts that introduce Cypher and cover graph imports if you're interested. There's also a GraphAcademy course about importing data that covers the basics.

We can examine a single to blog post to verify the graph schema model

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/cca9be1b-12ef-4413-9a09-dfe9cfc9885c)

Before we delve into analyzing the data, we'll utilize the NLP API to extract entities and relationships, known as "facts" in Diffbot's terminology.

o process the entities in the response and store the to Neo4j, we will use the following code:

You can try out Diffbot's online NLP demo on their website. Simply input any text, and it will show you the extracted entities and relationships. I've already input a sample content of an article we just imported into Neo4j, and we'll use the results for further analysis.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/750e7e0b-9e7e-405e-b2ba-8c401ad9240a)


The NLP API will find all the important things mentioned in the text and how they're connected. For instance, it might show that Jack Dorsey is the CEO of Block, a company located in San Francisco. Block deals with payments and mining. Another person mentioned is Thomas Templeton, who works with Jack at Block and has experience in computer hardware.
To process the entities in the response and store the to Neo4j, we will use the following code:


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/bbba37f0-d7a8-4542-b4b1-1f2019119db9)


This example will import only entities that have allowed types such as organization, person, product, and location, and their confidence level is greater than 0.7. Diffbot’s NLP API also features entity linking, where entities are linked to Wikipedia, Crunchbase, or LinkedIn, as far as I have seen. We also add the extra entity types as additional labels to the Entity node.

Next, we have to prepare the function that will clean and import relationships into Neo4j.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/b3c5df0d-fc04-48c5-885e-af28b7888263)

I've left out certain details from being imported. These details are listed in the skipProperties list. Instead of treating them as relationships between things, I think it's better to store them as properties of the things themselves. However, for now, we're just going to ignore these details during the import process.

Now that we've got the functions ready to import entities and relationships, we're ready to start working on the articles. You can send multiple articles at once. I've decided to group them in batches of 50 articles per request to make things easier to manage.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/48470954-5387-4fbc-9fe4-749a055a7e16)

By following these steps you have successfully constructed a knowledge graph in Neo4j. For example, we can visualize the neighborhood of Jack Dorsey.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/8a8866c2-fd65-4e47-9a3e-1bf229c68f85)

The NLP tool picked up that Jack Dorsey is the CEO of Block and has connections with Alex Morcos, Martin White, etc. But not all the info it extracted is accurate.

There's a funny error where it identified Elon Musk as an employee of Dogecoin, which isn't too far from the truth in a way. I haven't adjusted the confidence levels for facts yet, but you could raise the threshold to cut down on the mistakes. However, it's a trade-off between getting everything right and not missing anything.
This is just a small chunk of the overall picture. There's so much info available that it's tough to decide what to show.

ANALYZE OF GRAPH
In the final part of this post, I'll show you some example ways you could use a knowledge graph like this. First up, we'll check out the timeline of the articles


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/9f6096b2-026f-41b3-b975-c319282c89ac)


RESULT


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/247c98e7-d917-4b5d-99e5-2d0313e0a6fb)


There is between 150 to 450 articles per day about cryptocurrencies around the world which backs my initial statement about that volume being too much to read. Next, we will evaluate which entities are most frequently mentioned in articles.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/e921509f-1b1b-45d8-bb74-9cf5495a4b4c)


RESULT

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/82d32df5-2927-4fed-86a2-e465591d9a02)


As you would expect from articles revolving around cryptocurrencies, the most frequently mentioned entities are:

cryptocurrency
bitcoin
Ethereum and
blockchain
The sentiment is available on the article level as well as entity level. For example, we can examine the sentiment regarding bitcoin grouped by region.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/656afd08-95a4-42fb-9082-6ce045a0e764)


REASULT

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/6a81c031-7d4d-41ff-be30-cddafdaa4dde)


The sentiment is on average positive, but it heavily fluctuates between articles based on the standard deviation values. We could explore bitcoin sentiment more. Instead, we will examine which persons have the highest and lowest average sentiment in and also present in most articles in North America.
![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/983ff315-fbf1-4ec3-8b26-972a14826a5e)\
RESULT

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/6d19453a-3b96-4515-8f35-f27bc2790599)

Now, we can explore the titles of articles in which, for example, Mark Cuban appears.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/26096c70-4e46-4bbf-9594-8c997bc6a3c7)

While the titles themselves might not the most descriptive, we can also examine which other entities frequently co-occur in articles where Mark Cuban is mentioned.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/0bffc188-58e0-4171-af22-b087497f79a2)

RESULT


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/d6cc8162-3c41-4a31-87ba-f4196b6495c2)

Not surprisingly, various crypto tokens are present. Also, the Dallas Mavericks appear, which is the NBA club that Mark owns. Does Dallas Mavericks support crypto, or do reporters like to state that Mark owns the Dallas Mavericks, that I don’t know. You could proceed with that route of analysis, but here, we’ll also look at what facts we extracted during NLP processing.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/5dfbde3a-bfe3-4051-bc05-d6785dcf0e7c)

RESULT


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/59b8e6b0-6c56-433d-9c49-26b7cc81038d)

Next, we will quickly evaluate the article titles where Floyd Mayweather appears, as the average sentiment is quite low.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/59e72d90-813b-47d3-82ef-e974d71ebb00)

RESULT


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/e69190f3-1a20-49c4-854c-0e083bf4eb69

It seems that Kim Kardashian and Floyd Mayweather are being sued over an alleged crypto scam. The NLP processing also identifies various tokens and stock tickers, so we can analyze which are popular at the moment and their sentiment.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/e6be5ee5-7681-4a88-b831-73b98d215836)

RESULT


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/52457f6d-85e0-4f6a-a351-bdb5a590149d)

I have only scratched the surface of the available insights we could extract. For the end, I’ll just add two visualizations and mention some applications you could develop.


![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/6626f4f8-7809-4ccf-8573-964dd7fc2d0f)

For example, you could analyze the market by looking at relationships like COMPETITORS, ACQUIRED_BY, SUPPLIERS, etc. On the other hand, you could focus your analysis more on the persons in the graph and evaluate their influence or connections.

![image](https://github.com/ABHHI88/Monitoring-the-Cryptocurrency-Space-with-NLP-and-Knowledge-Graphs/assets/116937921/f6ee2515-b74b-4427-aabc-a4b61219054f)\

CONCLUSION
I've only just started exploring what we can do with this data pipeline. As I mentioned, you could keep an eye on news about your company, your competitors, or the entire industry. You could even try predicting future events, like company acquisitions. And don't forget, you could use the extracted data to power machine learning models for things like predicting crypto trends. There's a lot of possibilities!



































