# LangChain Prompts

This repository contains the concepts and code implementation for managing **Prompts** in LangChain.

## Overview
While the previous video covered the **Models** component, this module dives deeply into **Prompts**, explaining why hardcoded strings fail in scalable LLM architectures and how LangChain's Prompt Templates structure, manage, and optimize inputs for Large Language Models (LLMs).

---

## Table of Contents
1. [Why Prompt Templates?](#why-prompt-templates)
2. [Key Concepts Covered](#key-concepts-covered)
3. [Implementation Guide](#implementation-guide)
   - [1. String Prompt Templates](#1-string-prompt-templates)
   - [2. Chat Prompt Templates](#2-chat-prompt-templates)
   - [3. Message Placeholders for Chat History](#3-message-placeholders-for-chat-history)
4. [A Note on LLM Hyperparameters](#a-note-on-llm-hyperparameters)

---

## Why Prompt Templates?
In a real-world application, user inputs are rarely fed directly into an LLM. Instead, we bundle the user's specific request with dynamic context, system instructions, and structural boundaries. 

Instead of using raw Python f-strings, LangChain provides `PromptTemplates` which offer:
* **Modularity:** Easy to update instructions without breaking the application logic.
* **Composition:** Seamlessly stitching together multiple prompt components.
* **Integration:** Direct compatibility with LangChain Expressions Language (LCEL).

---

## Key Concepts Covered

* **`PromptTemplate`:** Used primarily for completion models (standard string input -> string output).
* **`ChatPromptTemplate`:** Specifically designed for chat models where structural roles matter (System, AI, and Human roles).
* **`MessagesPlaceholder`:** A dynamic structural component used to inject a full sequence of historical text messages (like a `chat_history` list) inside a custom prompt framework.

---

## Implementation Guide

### 1. String Prompt Templates
For non-chat style LLMs where you want to format strings dynamically using input variables.

```python
from langchain_core.prompts import PromptTemplate

# Defining a template with placeholders
template = "Tell me a joke about a {topic} in {language}."

prompt_template = PromptTemplate(
    input_variables=["topic", "language"],
    template=template
)

# Formatting the prompt dynamically
final_prompt = prompt_template.format(topic="programming", language="Hindi")
print(final_prompt)