---
slug: /
sidebar_position: 1
---

# Introduction

DevChat is an *open-source platform* that empowers developers to leverage AI for code generation and documentation.

## Why DevChat

While there are many AI coding tools available, we developed DevChat based on our practical insights gained from generating hundreds of thousands of lines of code. DevChat makes the following two distinctive design choices.

### Manual control of prompt context

**Precise control over context is the key to effective AI use.**
For instance, suppose you want AI to generate a few test cases for a function.
The bottleneck doesn't lie in crafting the request itself or in embedding instructions to AI, such as "you are a great tester."
Rather, the required information for the request, referred to as the *context*, is the most critical factor.
In this scenario, the context may encompass not only the function under test but also any other major function it calls, which can impact the test cases.
Additionally, the context might include a working similar test case to help the AI understand and replicate the settings and format of a test case in your specific environment.

We find that most other "intelligent" or "automatic" tools tend to over-guess what a user needs to put into a prompt, with the intention of reducing the user's workload.
This typically results in more noise than LLMs can efficiently handle.
The unstable effectiveness of those tools is a major reason why many developers are skeptical about AI's value in coding.
DevChat gives the control back to developers and streamlines the context building proces.
In practice, human developers remain the pilots, and AI can be truly effective only when provided with a clear request and appropriate context.

### Simple mechanism to extend

**You don't have to learn a new framework of a specific programming language to extend AI for your need.**
Prompts should be visible and easily editable to users instead of being hidden in a complex framework.
Adjustments to system-default prompts are common.
Take Python that has PEP

Bring your own prompts, and build a library of what works for you and your team. Easily integrate your own prompt templates into DevChat, avoiding significant engineering effort or a steep learning curve. You don't need a complex framework to make AI work for you. All it takes is a standard editor operating on your filesystem.

## Practical Views

DevChat's design choices are rooted in our practical views. If you agree with our perspectives outlined below, DevChat should be a perfect choice for you.

- **The bottleneck in harnessing AI's capabilities for coding lies in how to embed the right context in a prompt**. This isn't merely about the token limit of an AI model's input. Even with an infinite number of tokens, existing AI models would struggle to yield satisfactory results without a proper separation of concerns.
- **The value of prompt "engineering" is often overstated in AI coding**. While a well-crafted prompt template is helpful, it doesn't justify spending days or weeks of study. Instead, dedicate a few hours to create a few effective templates and share them with your team.
- The art of writing prompts is a skill honed through practice. It's not about templates or engineering, but about **refining individual communications for specific tasks on a case-by-case basis**.
- **Use AI only when it truly adds value**. Our misconception about AI's capabilities in reality is even a greater issue than hallucination of LLMs. What we need is a tool that boosts productivity, not merely an experiment.
