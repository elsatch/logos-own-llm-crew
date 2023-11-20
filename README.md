# Logos - Your own LLM Crew

Original version written 13 August 2023

TLDR; This is a conceptual framework for a personal crew of AI/LLM assistants

## Introduction

This document describes a self-hosted platform that can serve several LLM models to help you to do specific tasks.

Each model will be assigned a persistent name and field of work like calendar management, accounting, research assistant, etc. Models might be swapped depending of the performance in their particular fields. Ideally, models will be self-hosted but if the performance is not good enough, it might use cloud models too. To enable this flexible configuration, this platform will use LangChain to glue all processes.

## Architecture
This platform has several elements to fulfill its objectives:

- RapidAPI: to convert external calls to archive contents into archivebox calls.
- ArchiveBox: to store documents and websites in a consistent, standards compliant format.
- Chroma: a vector database that stores embeddings of the contents of ArchiveBox
- Text-generation-webui: to serve the LLMs
- LangChain: to orchestrate the calls between all elements
- Cron: to schedule periodic updates to the embeddings database

## Sample usage

You have three different assistants:

- Chloe: that saves all the invoices and offers summaries and insights about your accounting
- Martin: that helps you summarize research papers and offers insights about your bibliography
- Nomi: keeps track of all past and future appointments in your calendar
- Max: that transcribes vídeos and audios to text, providing key points and full text versions

Using your phone, you discover an interesting research paper. You share it using your system extensions, labeling it as research. This will trigger ArchiveBox to save the full PDF file, with the label research.

Periodically, LogosLLM platform will trigger a rebuild of the research articles, updating the embeddings on Chroma database.

User will talk to Martin bot on text-generation-webui, that is configured to consult by similarity of terms in the input among all stored research papers. When the user ask about the stored paper topic, it will retrieve the relevant fragments and link back to the original sources.

In the future, it will be possible to include several bots into the same conversation, like Chloe and Nomi to cross check your invoices and calendar appointments.

## Motivation

Humans use to interact with different people for different actions, so our brains might be more used to partition or associate certain tasks with different people in different contexts.

By splitting all input knowledge into different areas, we mimic the way we organize our daily routines, replacing a single omniscient oracle with several smaller specialized agents, that keep historical data access via the embeddings database.

Note: this platform might use either LangChain or Semantic Kernel to build its features.

