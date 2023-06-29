---
layout: post
title:  "Postgres as a Document store"
date:   2023-06-29 00:00:00 +0000
categories: database postgres document store llm
---
There is a lot of new development happening in the world of LLMs. Document stores are becoming an integral part of this ecosystem due to their critical role in fetching contextual data using RAG (Retrieval Augmented Generation). There are many state of the art document stores to help in this area. Postgres has been used a relational database along with JSON data format use cases. It also has capability to store documents acting as a complimentary document store. This is very helpful to get best of both worlds features.

Recently, I attended a event session on similar topic presented by EDB which can be checked [here](https://www.linkedin.com/events/flexibledocumentstoragewithpost7072639112662405120/theater/){:target="_blank"}. It's very insightful, in terms of explaining from basic indexes, features to document store based indexes, searches and their detail intricacies.

[pgvector](https://github.com/pgvector/pgvector){:target="_blank"} extension enables to use Postgres as a document store.