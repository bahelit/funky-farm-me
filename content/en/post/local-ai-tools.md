+++
date = 2023-09-20T09:14:48-04:00
description = "Run AI tools locally on your own hardware"
featured_image = '/images/posts/ai_generated/lavender_field.jpg'
tags = ["ai", "image generation", "LLM", "stable diffusion", "llama", "chatgpt"]
title = "AI Tools on Your Own Hardware"
+++

# Run AI Tools Locally 🤖

As the use of artificial intelligence (AI) continues to grow, I'd like to take a step back and appreciate the role that 
open source software has played in its development. Open source software has been instrumental in the development of AI, 
and it continues to play a key role in its future.  
<!--more-->

The use of AI has grown exponentially in recent years, with companies like Google, Facebook, and Amazon investing heavily 
in the development of AI tools. These tools are used for a variety of purposes, such as image recognition, and speech 
recognition. Now the AI generation tools are being incorporated into our daily lives through the use of personal 
assistants built into existing software people use every day such as office suites and image editing programs.

## Why Open Source Matters ⁉️

[Open source software](https://en.wikipedia.org/wiki/Open-source_software) is software that is made freely available and can be modified and redistributed by anyone. 
It is often developed collaboratively by a community of developers, who work together to improve the software and fix 
bugs.  

The infrastructure that powers the internet is built on open source software, without it the internet would not exist as
we know it today. Open source software has also played a key role in the development of AI, and it continues to play a
key role in its future.  

#### Privacy & Safety Concerns

With these tools functioning as personal assistants, there are privacy and safety concerns with the collection and 
storage off all this personal information. The data collected by these tools is often stored on servers owned by the 
companies that develop them, which means that they have access to your personal information. Your data is reviewed and 
used to improve the service but can also be used for targeted advertising or sold to third parties without your consent. 
In a worst case scenario the data can be stolen from the company and dumped on the dark web.  

#### Cost-Effective

One of the biggest advantages of open source software is its cost-effectiveness. This is particularly important for 
large language models, which require significant computational resources and can quickly add up in terms of costs. 
By using open source software, organizations can save money while still achieving their goals.  

#### Customizable

Another advantage of open source software is its customizability. Unlike proprietary software, where changes must be 
made by the vendor, open source software allows developers to modify the code to meet their specific needs. This means 
that individuals and organizations can tailor their large language models to fit their unique requirements, rather than 
being limited by what the software can do out of the box. This level of customization is particularly useful for 
training AI models on potentially sensitive datasets or for fine-tuning existing models for specific tasks.  

#### Community Support

Open source software also benefits from community support. When developers contribute to an open source project, they 
are not just contributing to the software itself, but also to the community around it. This leads to a wealth of 
knowledge and expertise being shared among developers, which can help to improve the quality and functionality of the 
software. In the case of large language models, this community support can be especially valuable, as these models are 
often complex and require specialized expertise to develop and deploy effectively. With open source software, 
individuals and organizations can tap into this collective knowledge and experience to ensure the success of their own 
AI projects.  

#### Flexibility

Finally, open source software offers flexibility in terms of deployment and integration. Traditional proprietary 
software is often designed to work within a specific ecosystem or infrastructure, making it difficult to integrate with 
other systems. In the case of AI software the proprietary software only runs on the cloud, which can be a problem for
organizations that want to run their AI models on-premises or in a hybrid cloud environment.  

For more information about open source see this Gitcoin article [A Brief History Of Open Source](https://www.gitcoin.co/blog/a-brief-history-of-open-source).  

## Open Source AI Tools 🛠️

Now that we got that out of the way, let's take a look at some of the open source AI tools that are available today.  

#### AI Tools Introduction

There are a couple basic things that will help in getting started with AI tools. The first is a basic understanding that 
there are the programs that run on the computer which we'll say is the "AI tool" and then there is the data that the 
AI tool uses, this is called the model and an AI tool could run multiple data models. This is a simplified explanation, 
but should alleviate some confusion when looking at the different AI tools.  

There are few different types of AI tools, with different ways of interacting with them such as through a command line 
or by using a web browser. The models containing the data can be found across the internet, and while the amount of 
options can be overwhelming the important thing to remember with the AI data models there are only a handful of base 
models as it costs millions to do the initial training. The wide variety of models found across the internet are 
versions of the base models that are modified to perform better on very specific tasks and shared back to the community.  

#### Text Generation Tools

Text generation tools are programs that generate text based on a given input, like ChatGPT for example. They can be used 
to generate text for a variety of purposes, personal assistant, automated customer service, and even creative writing. 
What these are doing in basic terms is pretty simple, they are completing the sentence based on what it has learned from 
the data model. One of the major differentiating factor between the different tools running on different machines is how 
much you can tell it at one time for it to work with to better complete the sentence. This is referred to as the token 
size, the larger the token size the more it can work with at one time.  

Depending on your computer skills and comfort level with the command line there are a couple different options for using
text generation tools. The easiest way to get started is a tool that uses a web browser for interacting with it, there 
are a couple different options for this. The other option is to use the command line, which is a bit more involved but 
can be more powerful.  

**Web Browser Text Generation Tools**
* [text-generation-webui](https://github.com/oobabooga/text-generation-webui) a web interface for text generation tools
* [catai](https://github.com/withcatai/catai) a web interface for 🦙 models where you talk to a cat 🐈

**Command Line Text Generation Tools**
* [llama.cpp](https://github.com/ggerganov/llama.cpp)
* [ollama](https://github.com/jmorganca/ollama)

#### Text Generation Models

Text generation models are the data that the text generation tools use to generate text. The models are trained on a 
large amount of text, and then the model is used to generate new text based on the input. The text generation models 
we're working with are known as large language models. A large language model (LLM) is a type of artificial 
intelligence (AI) algorithm that uses deep learning techniques and massively large data sets to understand, summarize, 
generate, and predict new content.  

For a more in-depth explanation see this video [What are Generative AI models?](https://youtu.be/hfIUstzHs9A?si=V0xVhBUj8xIdyhnF) by IBM Technology.  

**Large Language Models**
There can be tons of models to choose from but only a handful of them are base models, [llama2](https://ai.meta.com/llama/) is an open source
base model and many other models are based off of llama1 or llama2 with some modifications to make it better at a 
specific task. You can explore new models at [huggingface](https://huggingface.co/models), a website that hosts the models and provides a way to 
interact with them. Most of the tools to interact with the models will have a way to fetch the models from huggingface 
without having to download them manually.  

#### Image Generation Tools

Image generation tools are programs that generate images based on a given input, like Stable Diffusion. They can be used 
to generate images for a variety of purposes, like creating art or generating images for a website. What these are doing 
in basic terms is pretty simple, they are completing the image based on what it has learned from the data model.  

**Image Generation Tools** these support both the command line and web browser
* [Stable Diffusion WebU](https://github.com/AUTOMATIC1111/stable-diffusion-webui) Web interface for Stable Diffusion
* [SD.Next](https://github.com/vladmandic/automatic) Fork of Stable-Diffusion-WebUI - Advanced Implementation of Stable Diffusion
* [InvokeAI](https://github.com/invoke-ai/InvokeAI) Web interface for Stable Diffusion tailored for artists
* [Stable Studio](https://github.com/Stability-AI/StableStudio) Community interface for generative AI - The creators of Stable Diffusion

#### Image Generation Models

Like the text base models these have a base model that can generate all kinds of images based on a variety of styles, but
there are tons of specialized models that can do certain art styles or features better than the base model, such as ones
specialized in generating faces or landscapes. For tutorials on how to use Stable Diffusion to generate images see the 
[Stable Diffusion Art](https://stable-diffusion-art.com/) website, it covers a lot of the basics and is a great resource.

**Image Generation Models**
The image generation tools pull down the basic models from huggingface, but there are other models that are created by 
the community with specific art styles in mind. There are a couple different places to find these models, but I've 
primarily used just CivitAI for specialized models.  

* [CivitAI](https://civitai.com/) - A community of artists and developers working together to create new AI art tools
* [HuggingFace text-to-image models](https://huggingface.co/models?pipeline_tag=text-to-image&sort=trending) - Trending models for text-to-image generation  

## Wrapping Up 🎁
The AI tools are a lot of fun to play with and can be used for a variety of purposes even for profit. The tools are 
still in their infancy and will continue to improve on what they can do as well as ease of use as the community 
continues to work on them.  

Here are a couple example images generated with SD.Next.
Note: these are not the prompts to generate the images.

{{< figure src="/images/posts/ai_generated/sunset_waterfall.jpg" title="Sunset Waterfall 🌞" >}}  

{{< figure src="/images/posts/ai_generated/bird_on_a_flower.png" title="Bird on a flower 🌼" >}}  

{{< figure src="/images/posts/ai_generated/bird_zentangle.jpg" title="Bird and Wizard 🧙" >}}  
