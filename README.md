# 🤖 AI-Powered n8n Automation Suite: Content Curation, Job Hunting & Social Media Curation

[![n8n Version](https://img.shields.io/badge/n8n-1.0+-FF6C37?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![LLM Power](https://img.shields.io/badge/Powered%20By-Google%20Gemini-4285F4?style=for-the-badge&logo=googlegemini&logoColor=white)](https://deepmind.google/technologies/gemini/)
[![Spreadsheet Sync](https://img.shields.io/badge/Database-Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://www.google.com/sheets/about/)
[![Gmail Sync](https://img.shields.io/badge/Email-Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](https://mail.google.com/)
[![LinkedIn Integration](https://img.shields.io/badge/Publish%20to-LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://developer.linkedin.com/)
[![X/Twitter Integration](https://img.shields.io/badge/Publish%20to-X%20%2F%20Twitter-000000?style=for-the-badge&logo=x&logoColor=white)](https://developer.x.com/)

A comprehensive suite of six production-grade, enterprise-ready **n8n** automation workflows powered by **Google Gemini** LLMs. These workflows are designed to automate personal branding, professional career operations, email news curation, API event tracking, and job pipeline management.

Every workflow is fully generalized, safe for public distribution, and sanitized of all specific API Keys, personal emails, credential IDs, or spreadsheet locations. Import them directly into n8n, authenticate your credentials, and start automating immediately.

---

## 📂 Repository Contents

| Workflow File | Purpose | Trigger Source | Core Integrations |
| :--- | :--- | :--- | :--- |
| [`Auto Learning Journey Publisher.json`](./Auto%20Learning%20Journey%20Publisher.json) | Converts learning logs into structured LinkedIn updates and punchy X posts. | **Google Sheets** (every minute) | Google Gemini, LinkedIn API, Twitter/X API |
| [`Automated Social Media Content Generation.json`](./Automated%20Social%20Media%20Content%20Generation.json) | Curates and drafts insights for articles/links into social media updates. | **Google Sheets** (every hour) | Google Gemini, LinkedIn API, Twitter/X API |
| [`AI News Summarizer.json`](./AI%20News%20Summarizer.json) | Aggregates multiple RSS tech feeds into an AI-categorized morning briefing. | **Schedule Trigger** (Daily) | RSS Feeds, Google Gemini, Gmail API |
| [`Auto AI Internship Applier.json`](./Auto%20AI%20Internship%20Applier.json) | Reads open positions from a spreadsheet and drafts/sends structured cover letters. | **Google Sheets** (New Row) | Google Gemini, Structured JSON Parser, Gmail API |
| [`Automated LinkedIn Job Tracker with N8N.json`](./Automated%20LinkedIn%20Job%20Tracker%20with%20N8N.json) | Monitors LinkedIn job search RSS feeds, extracts skills, and drafts custom cover letters. | **Schedule Trigger** (Daily) | RSS Feeds, Google Gemini, Google Sheets API |
| [`AI News Summarizer Part 2.json`](./AI%20News%20Summarizer%20Part%202.json) | Combines RSS Feeds and SerpAPI Google News search query outputs into an expanded newsletter. | **Schedule Trigger** (Daily) | RSS Feeds, SerpAPI HTTP Node, Google Gemini, Gmail |

---

## ⚡ Detailed Workflow Breakdowns

### 1. Auto Learning Journey Publisher
Monitors your learning entries, summarizes raw study notes, and generates platform-specific professional updates.

* **Trigger**: Google Sheets (polls every minute).
* **AI Logic**: Extracts topics and achievements, generates a detailed LinkedIn update with tags, and creates an enthusiastically punchy tweet under 280 characters.
* **Flow**:
```mermaid
graph TD
    A[Google Sheets Trigger] --> B[Gemini - Article Summarizer]
    B --> C[Generate LinkedIn Post]
    B --> D[Generate X/Twitter Post]
    C --> E[Post to LinkedIn]
    D --> F[Post to X/Twitter]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style B fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style E fill:#0A66C2,stroke:#fff,stroke-width:2px,color:#fff
    style F fill:#111,stroke:#fff,stroke-width:2px,color:#fff
```

### 2. Automated Social Media Content Generation
Acts as a thought-leadership generator. Evaluates raw articles or developer blogs, synthesizes implications, and schedules updates.

* **Trigger**: Google Sheets (polls every hour).
* **AI Logic**: Summarizes article text, produces structural LinkedIn updates containing professional CTAs, and crafts short, high-impact tweets (within 30 words).
* **Flow**:
```mermaid
graph TD
    A[Google Sheets Trigger] --> B[Summarize News Article]
    B --> C[Generate LinkedIn Post]
    B --> D[Generate X/Twitter Post]
    C --> E[Create a Post]
    D --> F[Create Tweet]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style B fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style E fill:#0A66C2,stroke:#fff,stroke-width:2px,color:#fff
    style F fill:#111,stroke:#fff,stroke-width:2px,color:#fff
```

### 3. AI News Summarizer
Aggregates news items from multiple RSS tech portals, consolidates them, and feeds them into Gemini to build a beautifully structured morning briefing.

* **Trigger**: Cron/Schedule (runs daily at 10:00 AM).
* **AI Logic**: Merges feeds from diverse sources, filters articles, sorts them by logical headings (`AI NEWS`, `TECHNOLOGY UPDATES`), and highlights 3 items per section.
* **Flow**:
```mermaid
graph TD
    A[Schedule Trigger] --> B[RSS: Source A]
    A --> C[RSS: Source B]
    B --> D[Data Merger]
    C --> D
    D --> E[Data Aggregator]
    E --> F[AI Summarization Model]
    F --> G[Email Sender via Gmail]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style F fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style G fill:#EA4335,stroke:#fff,stroke-width:2px,color:#fff
```

### 4. Auto AI Internship Applier
Automates the initial outreach stage for internship applications by reviewing open pipeline spreadsheets and drafting personalized introduction letters.

* **Trigger**: Google Sheets (new application row appended).
* **AI Logic**: Evaluates role, company, student's details, and experience. Leverages a LangChain **Structured Output Parser** to format the output as strict JSON schema containing `{to, subject, body}`.
* **Flow**:
```mermaid
graph TD
    A[Google Sheets Trigger] --> B[Basic LLM Chain]
    C[Structured Output Parser] -.-> B
    B --> D[Send via Gmail]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style B fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style D fill:#EA4335,stroke:#fff,stroke-width:2px,color:#fff
```

### 5. Automated LinkedIn Job Tracker
Scrapes targeted job search feeds, parses specifications, identifies critical programming/architectural requirements, generates professional matching cover letters, and appends them to your tracking dashboard.

* **Trigger**: Cron/Schedule (runs daily at 1:00 AM).
* **AI Logic**: Consumes feed details, extracts specific technical requirements into list arrays, writes a cover letter, and updates your sheet records.
* **Flow**:
```mermaid
graph TD
    A[Schedule Trigger] --> B[RSS Read LinkedIn Jobs]
    B --> C[Basic LLM Chain]
    D[Structured Output Parser] -.-> C
    C --> E[Append/Update Google Sheet]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style C fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style E fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
```

### 6. AI News Summarizer Part 2
An advanced, multi-source compilation pipeline. Simultaneously monitors custom technology RSS Feeds and queries Google News via a custom SerpAPI HTTP request to dynamically consolidate tech, development, and upcoming event schedules into one daily intelligence digest.

* **Trigger**: Cron/Schedule (runs daily at 12:00 PM).
* **AI Logic**: Pulls RSS nodes and runs a custom Google News search query utilizing SerpAPI. Merges three separate inputs, aggregates data, and uses a Gemini 2.5 Flash chat model to draft comprehensive summaries and schedule lists.
* **Flow**:
```mermaid
graph TD
    A[Schedule Trigger] --> B[RSS: NormalTech]
    A --> C[RSS: AIBusiness]
    A --> D[SerpAPI: Fetch Google News]
    B --> E[Data Merger]
    C --> E
    D --> E
    E --> F[Data Aggregator]
    F --> G[AI Summarization Model]
    G --> H[Email Sender via Gmail]
    style A fill:#34A853,stroke:#fff,stroke-width:2px,color:#fff
    style D fill:#9B51E0,stroke:#fff,stroke-width:2px,color:#fff
    style G fill:#4285F4,stroke:#fff,stroke-width:2px,color:#fff
    style H fill:#EA4335,stroke:#fff,stroke-width:2px,color:#fff
```

---

## 📊 Database & Spreadsheet Schemas

For workflows that sync with Google Sheets, ensure your target worksheets are configured with the exact columns below:

### Workflow: `Auto Learning Journey Publisher`
* **Sheet Name**: `Sheet1`
* **Required Headers**: `Date` | `Topic/Module` | `What I Learned` | `Skills/Tools`

### Workflow: `Automated Social Media Content Generation`
* **Sheet Name**: `Sheet1`
* **Required Headers**: `text` | `Article Links`

### Workflow: `Auto AI Internship Applier`
* **Sheet Name**: `Sheet1`
* **Required Headers**: `Full Name` | `Email` | `Position Applied` | `Details` | `Experience (Years)` | `Skills`

### Workflow: `Automated LinkedIn Job Tracker`
* **Sheet Name**: `Sheet1`
* **Required Headers**: `Title` | `Link` | `Published Date` | `About Company and job description` | `skills` | `cover letter`

---

## 🛠️ Step-by-Step Deployment & Configuration

### Step 1: Import the Workflow
1. Log into your **n8n** instance.
2. In the left navigation, click on **Workflows** -> **Add Workflow** -> **Import from File**.
3. Choose one of the JSON files from this repository.
4. Click **Import**.

### Step 2: Configure Credentials
Set up credentials inside n8n for any integrations utilized by your imported workflow:

1. **Google Gemini API**: Create an API Key inside [Google AI Studio](https://aistudio.google.com/). Add a **Google Gemini(PaLM) API** connection in n8n.
2. **Google Sheets / Gmail API (OAuth2)**: Create a project on the [Google Cloud Console](https://console.cloud.google.com/), enable the target APIs, generate **OAuth 2.0 Client IDs**, and link them in n8n.
3. **LinkedIn OAuth2 API**: Register an app on the [LinkedIn Developer Portal](https://developer.linkedin.com/), enable sharing capabilities, and link via OAuth2.
4. **Twitter/X API**: Register your app on the [X Developer Portal](https://developer.x.com/) with **Read/Write** access, and configure user context connections.
5. **SerpAPI (If using Summarizer Part 2)**: Register an account at [SerpAPI](https://serpapi.com/) and obtain a free API key.

### Step 3: Link Your Resources
1. Create a spreadsheet in your Google Drive matching the matching column layout.
2. Copy the spreadsheet's ID from its URL.
3. Open the spreadsheet trigger/append nodes, replace `YOUR_SPREADSHEET_ID` in the **Document ID** parameter with your custom ID, and select the correct **Sheet Name**.
4. In workflows that use custom RSS feeds (Job Tracker / News Summarizer), replace `YOUR_LINKEDIN_JOBS_RSS_FEED_URL` with your feed's URL.
5. In email sender nodes, replace `YOUR_EMAIL@gmail.com` with your delivery address.
6. In `AI News Summarizer Part 2.json`, open the `Fetch Events` HTTP node and replace the query parameter value `YOUR_SERPAPI_API_KEY` with your SerpAPI key.

---

## 🔒 Security Best Practices

> [!IMPORTANT]
> **Zero Credential Sharing**
> 
> * These exported `.json` workflows **do not** contain any active auth accounts, passwords, or client secrets. n8n isolates all credentials in an encrypted internal database and references them using internal placeholders (e.g., `credentials-uuid-here`).
> * Any required raw API query strings (e.g., SerpAPI keys) are generalized as `YOUR_SERPAPI_API_KEY`.
> * Ensure your spreadsheet data files and local environment configuration sheets are ignored via the active `.gitignore`.

---

## 📄 License
This repository is open-source and available under the [MIT License](LICENSE).
