---
layout: post
title: How to Build a ChatBot Using Google Cloud
date: 2024-10-02 01:00:00-0400
description: 
tags: ChatBot, llm, Google Cloud, Vertex AI, Agent Builder, Vertex Search
categories: ChatBot, llm, Google Cloud, Vertex AI, Agent Builder, Vertex Search   
---

 Chatbot Design Document

#### 1. **Overview**

The purpose of this document is to outline the design and architecture of a chatbot application which automates customer support. The chatbot will be built based on Google Cloud's(GCP) services to handle customer queries, provide relevant information, and automate customer support tasks. It will use GCP's Vertex AI Agent Builder, Vertex Search, Dialogflow API, Generative AI Models(Gemini) and  various other services. 

Note: I Know there is a voice based customer support as well, for simplicity i am not including those solutions here. If you need Voice based solutions then the Simplest is to use features in Vertex AI Agent builder and Dialogflow for voice based input, with few configurations the same text based solution can be reconfigured. As of now, i proposing to use the voice data as well in building the chatbot by transcribing it into text. 

#### 2. **Objectives**

- Automate customer support and FAQ handling.
- Provide real-time, accurate responses using an LLM.
- Integrate with external knowledge bases and customer support systems.
- Support various deployment models (e.g., web-based, mobile, or in-app).

#### 3. **Key Requirements**

- ChatBot Framework: Vertex AI Agent Builder (GCP) with Dialogflow API
	- Vertex AI Agent Builder has an end to end features to build production ready chatbot applications. For example you can add Dialogflow API and Generative models which are immensely helpful in building chatbot application.  
- Embedding Models: _textembedding-gecko_ (GCP)
	- If the performance of the Embedding model is not high for our dataset, then we can fine-tune the model on our custom dataset to increase the accuracies of the embeddings. 
- **Language Model:** Gemini 1.5 Flash or Gemini 1.5 Pro
- Vector Database: Vector AI Data Stores
- RAG: Vertex AI  Search
	- Vertex AI Search is an Out of the box solution with little effort you could create RAG based embedding solutions. 
- Google Buckets: For storing all kinds of data
- Pub/Sub: For managing message traffic
- **Fallback and Escalation:** Generative Fallback 
	- In cases where the chatbot cannot handle a query, it should escalate to a human agent or provide alternative resources.
- **Monitoring and Analytics:** Dialogflow CX 
	- It has options where it Provides insights into chatbot performance, user engagement, and areas for improvement.
- Data Ingestion and Data Cleaning
	- Chat History Data from both text and audio.
	- Supporting Documents and Technical manuals. 
	- We clean the data and make ready so that it is passed to the data stores in vertex search service, so that it will embedded and stored in the vector database. 
	

#### 4. **System Architecture**

The Design choices for the chatbot is very carefully constructed such that most of the workflows of customer interactions is predefined unless it is a very complex cases. It will be a constrained interaction where majority(where ever the opportunity persists) of it is either buttons to select from or search from predefined list. This approach would reduce lot of unwanted interactions or abusing of the system. It will be lot of work initially but very worth in the long run.

This solution is fully intended to take advantage the power of llms. Since the llms are kind of black boxes and if something goes wrong in the chatbot, it is very difficult to debug, so for that reason where ever the opportunity persists i wanted to have deterministic intents and in other place leverage the power of llms. 

Note:
When Building Chatbots using Vertex AI Agent Builder there are 2 approaches you can choose. 
1. Vector AI Search and Conversation, which is much easier approach where you give all your data to it which will create a data store and make it available to the default chatbot it will build. We don't have control over the flow of the conversations, it will truly leverages the llms. 
2. Dialogflow CX with Generative models, this approach has much more flexibility. It has the best of both worlds where you can create deterministic intents and plugin generative model aswell. 

    

#### 5. **Flow of Operation**

1. Greeting Message: Initial greeting message along with multiple choice options to select is displayed. 
2. **User Input:** The user submits a response by selecting from the provided options.
3. User Input Parsing: Since the response is from pre-defined list, it is easy to route to the specific category and based on that it will output the appropriate response. Steps 2 and 3 are repeated until you reach to the point where customer has to input a free text query.
4. User Input: User Submits the free text query. 
5. **Context Check:** The Conversation Context Manager checks if there is any relevant context from previous interactions that should be included in the request.
6. **LLM Request:** The parsed query is sent to the Vector Search(RAG+Vector Database) to retrieve all the relevant information from customer chat database and supporting documentations. All of these informations are passed to the llms to get appropriate response. 
7. **LLM Response:** The LLM generates a response, which may include additional contextual information retrieved from the knowledge base.
8. **Response Display:** The formatted response is returned to the user via the UI.
9. **Fallback:** If the LLM is unable to generate a satisfactory response, the fallback system will either provide an default message or escalate the query to a human agent.
10. **Monitoring:** All interactions are logged for analytics and monitoring purposes.

#### 7. **Deployment Considerations**

	Since most of the services are from GCP, vertex AI does provide options to easily deploy the services and also it can scale well. There are definately limitations, if the application is very complex and scale of it really huge then we need to think of other solutions. 


#### 9. **Testing & Validation**

- **Unit Tests:** Test individual components like the NLP layer, context manager, and LLM integration.
- **Integration Tests:** Ensure smooth communication between LLM, retrieval system, and user interfaces.
- **Load Testing:** Simulate heavy user interaction scenarios to ensure scalability.
- **A/B Testing:** Test different versions of the chatbot response models and fallback systems for effectiveness.

#### 10. **Monitoring & Analytics**

- **Key Metrics:**
    - User satisfaction (via feedback or follow-up questions).
    - Query resolution rate.
    - Response time and latency.
    - LLM usage cost per query.
- **Tools:** AWS CloudWatch, Prometheus, or custom-built dashboards for monitoring chatbot performance.





