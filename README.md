# AI Job Application Automation

An AI-powered automation workflow that finds relevant job listings, evaluates them using LLMs, and automatically generates tailored cover letters.

Built using **n8n**, **OpenRouter**, and **Apify**.

---

## Features

- Automated job scraping
- AI-powered job relevance scoring
- Intelligent filtering of job listings
- Automatic cover letter generation
- Job tracking with Google Sheets
- Email notifications for strong matches

---

## Workflow Overview

Job Scraper → AI Scoring → Filtering → Cover Letter Generation → Google Sheets → Email Notification

---

## Tech Stack

- n8n (Workflow automation)
- OpenRouter (LLM inference)
- Apify (Job scraping)
- Google Sheets API
- Gmail API

---

## Architecture

This automation runs on a schedule and:
1) Scrapes job listings (Apify)
2) Scores each job against my resume using an LLM (OpenRouter)
3) Filters jobs based on a minimum score threshold
4) Generates a tailored cover letter for strong matches
5) Logs results to Google Sheets
6) Sends an email notification

mermaid
flowchart TD
  A[Schedule Trigger] --> B[Apify Run Actor]
  B --> C[Get Dataset Items]
  C --> D[Limit Jobs]
  D --> E[HTTP: OpenRouter Job Scoring]
  E --> F[Code: Parse Scoring JSON]
  F --> G{IF total_score >= threshold}
  G -- False --> H[End / Ignore Job]
  G -- True --> I[HTTP: OpenRouter Cover Letter]
  I --> J[Code: Extract Cover Letter Text]
  J --> K[Edit Fields (Set)]
  K --> L[Google Sheets: Append Row]
  L --> M[Email: Notify Me]

## Example Output

Jobs are automatically stored in Google Sheets with:

- Job title
- Company
- Score
- Generated cover letter

---

## Setup Instructions

1. Import the workflow JSON into n8n
2. Configure credentials:
   - OpenRouter API key
   - Google Sheets OAuth
   - Gmail credentials
3. Run the workflow

---

## Future Improvements

- Auto-apply to job portals
- Resume tailoring using AI
- Slack / Discord notifications
- Job match analytics dashboard

---

## Author

Dadul Rishan
