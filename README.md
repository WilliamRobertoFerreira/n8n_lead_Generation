# AI-Powered Lead Generation & Enrichment Workflow (n8n)

![n8n](https://img.shields.io/badge/n8n-121_189_163?style=for-the-badge&logo=n8n&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-8E75B2?style=for-the-badge&logo=google&logoColor=white)
![SerpApi](https://img.shields.io/badge/SerpApi-4A85C3?style=for-the-badge&logo=googlechrome&logoColor=white)

An automated n8n workflow designed to scrape leads from a website, enrich them with valuable business data using a Gemini-powered AI agent with real-time web search capabilities, and deliver a formatted report via email.

This project serves as a powerful example of how to build an "AI Agentic Workflow" where different AI agents with specific roles (Parser, Researcher) and tools (Web Search) are orchestrated in a pipeline to perform complex automation tasks.

## Author

-   **William Ferreira**
    -   [![LinkedIn](https://img.shields.io/badge/LinkedIn-williamrferreira-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/williamrferreira/)

## Core Features

-   **Automated Web Scraping**: Fetches the initial HTML content from a target URL.
-   **AI-Powered HTML Parsing**: A Google Gemini agent intelligently parses the raw HTML to extract an initial list of company leads and structures it into clean JSON.
-   **Individual Lead Processing**: The workflow processes each lead one by one for focused and accurate enrichment.
-   **Real-Time Data Enrichment**: An "Enrichment Agent" uses the **SerpAPI** tool to perform live Google searches for each lead.
-   **Hierarchical Search Logic**: The agent follows a multi-step validation process to find critical data like the Brazilian company ID (CNPJ) and contact email, ensuring data quality:
    1.  First, it performs a precise search combining the company name and address.
    2.  If that fails, it performs a broader search on official business registry websites.
    3.  It validates the results to avoid mismatches.
-   **Automated HTML Report Generation**: A final AI agent compiles all the enriched data into a clean, professional HTML report.
-   **Email Delivery**: The final report is automatically sent to a specified recipient using Gmail.

## Tech Stack

-   **[n8n.io](https://n8n.io/)**: The core automation platform.
-   **[Google Gemini](https://gemini.google.com/)**: The Large Language Model (LLM) used for parsing, enrichment logic, and report generation.
-   **[SerpAPI](https://serpapi.com/)**: The tool that provides the AI agent with real-time web search capabilities.

## Getting Started

To get this workflow running in your own n8n instance, follow these steps.

### Prerequisites

1.  A running **n8n instance** (Cloud or Self-Hosted).
2.  An **API Key from Google AI Studio** for the Gemini model.
3.  An **API Key from SerpAPI**.
4.  **Gmail API Credentials** (OAuth2) configured in your n8n instance to send emails.

### Installation

1.  **Copy the Workflow JSON**: The entire content of the `workflow.json` file in this repository is the workflow.
2.  **Paste into n8n**: Open your n8n instance, create a new blank workflow, and simply paste the copied JSON onto the canvas. The entire workflow will appear.

### Configuration

Before you can run the workflow, you must link your credentials to the correct nodes:

1.  **Google Gemini Credentials**:
    -   In your n8n instance, go to **Credentials** and add your Google Gemini (PaLM) API key.
    -   In the workflow, find the three nodes named **"Google Gemini Chat Model"** and select your newly created credential for each of them.

2.  **SerpAPI Credentials**:
    -   Go to **Credentials** in n8n and add your SerpAPI key.
    -   Find the **"SerpAPI"** node and select your SerpAPI credential.

3.  **Gmail Credentials**:
    -   Go to **Credentials** in n8n and add your Gmail (OAuth2) credential.
    -   Find the final node named **"Send a message"** and select your Gmail credential.
    -   **Important**: In this same node, update the **"To"** field with your desired recipient's email address and customize the **"Subject"** field.

## Usage

Once the workflow is installed and all credentials are configured, you can run it:

1.  Open the workflow in the n8n editor.
2.  Click **"Execute Workflow"**.

The workflow will execute all the steps, and upon completion, the specified recipient will receive an HTML email containing the list of enriched leads.

## Customization

This workflow is a template and can be easily adapted for your own needs:

-   **Change the Target URL**: Modify the URL in the **"HTTP Request"** node to scrape a different website.
-   **Adjust the Prompts**: Edit the prompts in the **"AI Agent"** nodes to extract different data fields or enrich with other information (e.g., social media links, company size, etc.).
-   **Change the Final Action**: Replace the **"Send a message"** (Gmail) node with another node to send the data to a different destination, such as:
    -   A Google Sheet
    -   A Slack channel
    -   A CRM like HubSpot
    -   A database like PostgreSQL
