# Trump-Chat-Bot
In collaboration with Nick Olivier, Jacob Reyes, and Stew Williamson

# General Information
With the recent revelations about Russian bots tampering in the United States elections, we wanted to learn more about what a “bot” is and how they can be trained to talk like people do. To narrow our scope, we made a Trump bot. After some research into what the industry best practice is, we decided to use a recurrent neural network to teach our bot how to speak. At the end of the project, our model returned semi-coherent responses. In future iterations, we plan first teaching the chatbot to speak using regular speech text and then “Trumpify” the responses by re-training on Trump's speech patterns.

Even though our goal was academic, there are many real world applications to creating a Trump bot. One, the Russian bots that tampered with the last presidential election showed the power behind anonymity on social media gives. Bots were used to create confusion and stir up civil unrest. Using a Trump bot, versus the general bots the Russians used, could create more unrest and confusion about the President’s stances. Another, less nefarious, use case is that the White House could use a Trump bot to personalize automated responses to his constituents. 

TrumpBot 2020’s main goal is to come up with ad hoc responses to questions so that people can ‘chat’ with it. These responses need to be fed through the model so that the bot is actually ‘talking’ and not spitting out a rule based response.

# Development Process
We utilized beautifulsoup, the python web scraping package, in order to get the text data needed for training and testing our model. We scraped interviews, rallies, transcripts of video logs, speeches, press conferences, and White House Press briefings. Our data ranges from the early 1980s to 2018. Web scraping took more time than expected because there was not a full consolidated list of all Trump data in one place. In fact, we had to scrape a multitude of different sources that each had a couple texts hosted on that particular website. It was also difficult to find the websites that did have his information because there are a couple popular ones that are easy to find and the rest are obscure sites. Some of the texts that we scraped were official versions of a speech written by aides and did not take into consideration the actual words spoken. This means that these texts were a slightly different speech pattern than the the transcripts of his speeches and interviews. We also had a hard time finding conversational data. During our research, we learned that conversational data helps the machine learning algorithm decide how to respond to a user. While we did find a few interviews, we needed more samples and needed to find a way to show the difference between a question and response.

After web scraping all the different data sources, we compiled all the text documents into one large document. Then we began to clean our data. The first step was removing all non-speech from the document. This included removing hyperlinks, captions, picture metadata, amoung others. One of the decisions we made about how to clean data was about contractions. Normally in natural language processing contractions are either split into their component parts (don’t → do not) or have the apostrophe removed (don’t → dont). However, we felt that contractions are an important part of spoken word and should not be removed or changed. “Don’t” has a different connotation than the more formal “do not” and therefore, we chose not to remove any apostrophes that had a letter both right before and right after it.

The Trump data we looked at also used a lot of abbreviations that are common in politics (FLOTUS for First Lady of the United States, GOP for the Republican Party/”the Grand Old Party”, SC for Supreme Court, etc) but not used in regular conversations. We were worried that the model would pick them up as regular words and would pepper these abbreviations in as it would a regular noun. We still decided to leave the abbreviations unchanged because we felt that since we limited our scope to mimicking Trump, instead of an average person, the increased use of the political abbreviations would not be detrimental to the overall model.

That leads to the next question we faced which was how to deal with proper nouns. Trump text has a lot of proper nouns because he is often talking about foreign policy, decision makers, or countries. Often times whole speeches would be about one individual/country. We were not sure what the best approach to proper nouns were, but we decided to keep them in the data because they provide important context to the topics that Trump could talk about. 

Another important decision we had to make was about punctuation. Punctuation is important to sentence structure and helps us understand what others are saying. Therefore, we debated keeping punctuation as tokens. However, we decided not to do this because we felt it was more important to get coherent thoughts out first and then worry about proper grammar.

During the process of building our generative model, we used a few different approaches. We started by using an existing python library called PyTorch which enabled us to quickly build a generative model. This gave us the opportunity to work with a generative model without having to write much code. We quickly realized that although the PyTorch model worked, it was severely lacking in the coherence of the response that it was providing. We then began to develop an RNN using Keras in TensorFlow. The main reason we chose to use an RNN for our model is because our chatbot requires a generative approach. It must consume content, analyze, and generate new content to reply to the user. One of the most common issues with RNN (that we encountered) is the vanishing gradient problem. We were able to overcome this obstacle by utilizing gated recurrent units (GRU’s). GRU’s are trainable parameters that we used to instruct our model on which information it should “remember” or “forget”. This approach is similar to Long Short-Term Memory (LSTM) networks. 
Once we built an initial RNN, we iterated it to help increase the coherence of our output. After a few iterations we began to realize that we did not have enough processing power to continue to add to our model. After a while we had to stop development because the model would take hours to process. 

# Lessons Learned
One major obstacle we faced was a lack of computing power. As we built out our RNN the computational power required continued to increase. In the future when working on a building a model like this we will obtain the resources ahead of time so that we can have time to integrate them into our process. Another obstacle was not having enough text to train our model. Reflecting on our project, we should have used larger amounts of text to train the model to produce coherent sentences. From that point we could integrate Trump’s dialect to the model. Training the model strictly on one person's speech did not provide enough training data. 

# Potential Next Steps
A.	Increase the training corpus
One of the largest obstacles encountered throughout this project was the limitations of available speech transcripts attributable to President Trump. Although President Trump is a relatively well-documented and voluble individual, the data available was still vastly insignificant to effectively train a recurrent neural network. This issue was further compounded by the structural requirements of the training data which needed to be of a conversational nature in order to educate the chatbot on the back-and-forth order and flow of human conversation. The authors believe that the training corpus could be expanded to include conversational transcripts from additional public figures of a similar group (U.S. presidents or real estate moguls for example) to improve the training approach whilst maintaining the topics of speech and general vocabulary that a user might expect from conversing with a Trumpbot.

B.	Improve grammar and punctuation
In its current state, Trumpbot is significantly lacking in grammatical acumen. The lack of punctuation and grammatical correctness in Trumpbot’s responses could be rectified by incorporating a grammar and punctuation corpus into the training process. Rather than building from scratch, the most practical approach would be to adopt one or several of the punctuation and grammar corpuses now readily available online. An alternative approach would include utilizing a grammar checking tool as a feedback loop in which Trumpbot outputs would be verified by the grammar checking tool and the model would then be either rewarded or penalized based on the grammatical soundness of the output.

C.	Build a companion bot
A comical yet intriguing enhancement would be to create a companion bot modeled after a political opponent of the Democratic party with the ultimate goal of having the bots debate. Besides being entertaining, this would provide the additional scrutiny of having one bot’s output become the other bot’s input and vise versa. This symbiotic relationship between the bots places even greater severity on the quality of data inputs and training approaches. By introducing each bots output as a feedback loop into the companion bot, it would be interesting to observe the conversational progression and whether English grammatical principles continued to be followed or whether the bots developed their own conversational system with a unique set of rules and grammar protocols.

