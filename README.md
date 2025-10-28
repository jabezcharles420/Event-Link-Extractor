# Event Data Extractor & Enrichment Workflow

This n8n workflow is designed to automate the process of gathering detailed information about events. It starts with a list of event URLs, scrapes each one, and uses a powerful two-stage AI process to extract and then enrich the data before saving it in a structured format.

##  workflow Overview

The workflow performs the following steps:

1.  **Manual Trigger:** The workflow is initiated manually.
2.  **Read Input Sheet:** It fetches a list of items (presumably containing event URLs) from a source Google Sheet.
3.  **Loop & Scrape:** It iterates over each item from the sheet.
    * It uses **Firecrawl** to scrape the content of the event URL.
    * A Code node extracts basic metadata from the scraped page.
4.  **Enrichment (2-Stage AI):**
    * **Stage 1 (Extraction):** The first AI Agent (using OpenAI) attempts to extract a comprehensive set of event details (like venue, ticket price, capacity, etc.) directly from the scraped data.
    * **Stage 2 (Enrichment):** The second AI Agent (using OpenAI + **Tavily Search**) takes the output from Stage 1. If any fields are marked "Unknown," this agent uses its web search tool to find the missing information online.
5.  **Write Output Sheet:** The final, enriched JSON object containing all the event details is appended as a new row to a target Google Sheet.

## Features

* **Automated Scraping:** Uses Firecrawl to scrape event web pages.
* **AI-Powered Extraction:** Employs a Langchain agent with OpenAI to parse scraped data into a structured JSON.
* **AI-Powered Enrichment:** Uses a second agent with Tavily web search to intelligently find and fill in any missing event details.
* **Google Sheets Integration:** Fully integrated with Google Sheets for both reading inputs and writing structured outputs.

## Credentials Required

To run this workflow, you will need to provide credentials for the following services:

* **Google Sheets:** To read the input URLs and write the final data.
* **OpenAI:** To power the AI extraction and enrichment agents.
* **Tavily AI:** For the web search capabilities of the enrichment agent.
* **Firecrawl:** For scraping the event web pages.

<img width="1234" height="350" alt="image" src="https://github.com/user-attachments/assets/0c3cc369-9bd7-4fcd-abb4-47f7e00f4221" />

