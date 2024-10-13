Project Architecture
====================

Pricer of exile project consists of two different flows the first one is dedicated to training the AI model and the second one in charge of the "live" flow. We decided to create multiple different components in different technologies to support this flows.

![Price of Exile Architecture](/assets/architecture/pricer-of-exile.jpg)

Training Flow
-------------

The aim of the training flow is to take objects on the market and their prices, then categorise them and train our artificial intelligence model to answer the question: 

`Is my object worth something?`

### Data Aggregation and Parsing

> More details [Here](Components/data_aggregation_and_parsing.md)

This involves several stages, the first is retrieval of listed items from the APIs exposed by Grinding Gear Games. This task is carried out by a small script written in NodeJS: [crawler-of-exile](https://github.com/PricerOfExile/crawler-of-exile), which requests an API that exposes public market information and persists it in files without any transformation. Note: at the time this script was run, this represented more than 300 gigabytes of data.

Data persisted in this way must now be filtered and transformed. Filtered because we only need listed items with a price, and because we only focus on specific items. And transformed because in these files the main representation is textual as the initial purpose of this API is to display items to final user. It's the [parser-of-exile](https://github.com/PricerOfExile/parser-of-exile) component which is in charge of these part of the folw : filter priced `accessories` items, transform them into standard representation and persist them in JSON file.

### Model Exploration and Training

> More details [Here](Components/Model/model.md)

These standardized priced objects are loaded and used by our last training component [model-exploration-v2](https://github.com/PricerOfExile/model-exploration-v2). This is a python project using given data and some python libraries dedicated to IA to train and produce our custom model.  

Live Flow
---------

### User Interaction

> More details [Here](Components/interface.md)

This flow will support the main use case of the project. A player want to know the `tier`/`rating` of a specific item. For that he will Ctrl+C this item, and our component [poe-pricer-front](https://github.com/PricerOfExile/poe-ai-pricer-front) written in Electron will intercept this command and the textual representation of the item to send it to the next part of the chain.

### Data Parsing

> More details [Here](Components/data_aggregation_and_parsing.md)

Again we have another textual representation of an item, so we use the same component [parser-of-exile](https://github.com/PricerOfExile/parser-of-exile) in order to translate it to our `standardized` item.

### Rating Prediction

This transformation done, we want to predict the rating of the item. This prediction is done by our last component [poe-exposed-model](https://github.com/PricerOfExile/poe-exposed-model) : a python component loading the IA model trained by [model-exploration-v2](https://github.com/PricerOfExile/model-exploration-v2). 

The prediction will go all the way back up the chain to be displayed to the user, who will know how `Pricer of Exile` rates his item. 

