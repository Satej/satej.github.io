---
layout: post
title:  "Insights from Pydantic for LLM Workflows - Deeplearning.ai"
date:   2025-08-17 00:00:00 +0000
categories: pydantic llm worflow schema validation deeplearning ai
---
Thanks to the course on [Pydantic for LLM Workflows](https://learn.deeplearning.ai/courses/pydantic-for-llm-workflows/lesson/w6ohb/welcome-to-pydantic-for-llm-workflows){:target="_blank"} course. I learnt a lot in a short time. I had previous experience and some use of validation of json being passed to LLMs by using Pydantic to improve the schema validation autoamtion was another level of learning. I would recommend to take this course. The application extends to many use cases and the imagination is the only limit. Some of the ones I can think of is data schema validation and automating and self-servicing data engineering request changes being one of them.

Insights gained:
1. Pydantic library for input validation and feedback looping through LLMs to correct errors and get the output in the right format.
2. This is also helpful to automate system to system calls which have a input contract.
3. Trick to improve the prompt through self-analysis and passing the model schema as hint.
4. Use of [instructor library](https://python.useinstructor.com/#quick-start-extract-structured-data-in-3-lines){:target="_blank"} as an abstraction to use to call any llm provider in the backend with a consistent api and responding with pydantic model output.
5. This can be extended through use of [Pydantic AI](https://ai.pydantic.dev/){:target="_blank"} library which helps to use agentic ai with schema validation on top of pydantic reducing the need to write feedback logic.

Below you can find a snapshot of [my course completion certificate](https://learn.deeplearning.ai/accomplishments/997338a2-c678-4ff1-972e-def65e7f6214?usp=sharing){:target="_blank"}.

![Pydantic for LLM Workflows Course completion certificate](../assets/post_images/2025-08-17/pydantic-for-llm-workflows.png)
<object data="../assets/post_images/2024-10-11/multi-modal-llama-3-2.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="../assets/post_images/2024-10-11/multi-modal-llama-3-2.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="../assets/post_images/2024-10-11/multi-modal-llama-3-2.pdf">Download PDF</a>.</p>
    </embed>
</object>
