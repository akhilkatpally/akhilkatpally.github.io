---
layout: post
title: Understanding llm fine-tuning step to understand prompt engineering
date: 2024-08-01 01:00:00-0400
description: To be successfull at prompt engieering, understanding what went into fine-tuning llm is crucial. 
tags: llm fine-tuning, prompt engineering, ai
categories: ai, llm, fine-tuning, prompt engineering 
---

Problem: How to ace prompt engineering? 
Solution: Large Language Models are black boxes, unless we try different prompts we don't know which prompts produce good results. There are many suggestions online on how to write good prompts either directly from model providers or practioners. When compared to general programming which is very standardized, where we have syntax and we have the help of api's to write code. It is bit frustating to interact with llm, my gut feeling is we all humans like standardization and reliability. 

Pre-trained models are practically unuseable unless they are fine-tuned. It is this fine-tuning step which introduced the prompting. There are two ways you could solve this issue ..... 

First, if all the model providers could release the major prompts/instructions which they have used in the fine-tuning datasets. If we know all the instructions which they have used to fine-tune it then using those prompts will give good results. All the initial versions of the models they have described/released the fine-tuning datasets. It is highly unlikely given the IP Concerns they would release those information now.  

Second, Reverse Engineering the fine-tuned model to understand the major prompts/instructions would be very helpful. How would you do that is the major concern, machanistic interpretability or asking the model itself or altogether using agents. Using Agents to divide the big problem into multiple small problems and using agents to solve each small problem and correcting based on the feedback seems to be the go to workflow now. 


 


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="https://www.youtube.com/watch?v=ewRjZoRtu0Y" class="img-fluid rounded z-depth-1" %}
    </div>

</div>
