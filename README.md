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

