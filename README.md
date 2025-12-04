# Automated Lead Processing & Enrichment System

> An intelligent B2B lead qualification system built with n8n that automatically captures, researches, scores, and syncs qualified business leads from Lightspeed to Pipedrive CRM.

![n8n](https://img.shields.io/badge/n8n-Workflow-EA4B71?logo=n8n)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI-4285F4?logo=google)
![Pipedrive](https://img.shields.io/badge/Pipedrive-CRM-0BB04B.svg?logo=data:image/png;base64,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)
![Lightspeed](https://img.shields.io/badge/Lightspeed-E--commerce-000000.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAADZ0lEQVRYhaXXS2heRRQH8J9BSigSJJRwkaEEoUZ8VCulC5FaMEFxIxZfiIriA+qrtVpKkVAkBFdaLeLalY/ahQiC2LqwitaViKUiLaXoUC6lBClBQgnBxcynk4/vcb8vZ3Xnf+/8/zNnzpxzLmuwOoSNdQija+EYWctkvIM31kJw1bAT6xC24zv8g6kqxjgMz1AeqEMYkXYP6/HSMDxDLwBPYGsx/mvYBQx8BHUI63EG12XoLG7GKBarGFcG4RvGA/sLcXitivEK5vD0oGQDeaAOIeAP6dzhG9yLm/ArFrCpivFyU85BPfB2Ib4s7Z4UkFdjAq8OQth4AXUI2/B4AX1YxXi6DuF+3DcMJw2PoA4BvsddGbqEKSziN9yQ8QVswt9Ng7Hpah8pxOFgFeMCXi7EYTbje+sQSq90tb4eyLn+d0xm6BS2YFwKyGvb8A0Zv4BbqxiXe/E38cCeQhx2Z9K5QpwUkMuYxxhuxIv9yHt6oA5hQko6Yxn6oorxwTqEzfil2MCXVYwP1CFsxc8FviDViUvdNPp5YK4QX8LrOSDfL+Ze6YKTjumtXgJdF5B3+VwBvVfFeA47saMNPytd0Ts7UL1Qh3BLN52uR1CHcAzTeXhBunbLVgdknfGVjIcCH8e6PD6OmapDxe7ogbz76QI6UMW4iL1WB+SbOe3uL8RhHz4oxtO4vZNWtyO4vnhewtH8/GQbfqQOYdLqrugkPsZnbZyTOli3BZwunkelnZOCssT3SHWg1ReuSNd0BQd7cP5nvWLgczyUh4vSWdf4CdsyvlSIw0dVjM/k+vBVgR+tYny4k06va7gvC8A1mM872118U4pfxoE6hHU4VOBLUox0tK4LqGI8j8MF9FQdwh1VjCfxaYcp81WMtVSOy/pwOF/fjtYvE45JmXAiQydwNzZK167VG7TaslZ9aCWvi/o0KD0zYZ44W0DbsbOK8U//B+QyXsltWasOtGy2X3fUpBqOSHl/c4bO4bYqxsWc4RarGM/XIezAt8WmTmFLv2rYtCGZxrECOoFduSMaldr0Q1KwtmymivF4P+7GTWkdwid4rA1ekOKg/f/wSBXjo014B+nfnscPbdh4B/Ef8WxT0sYLyLVgBu9KJbjdruR39+RvG9lQP6d1CBukTngqQ2fwdRXjxUG5/gXjDRD1FVFwowAAAABJRU5ErkJggg==)

## 🎯 Overview

This automation system eliminates manual lead qualification by using AI-powered research to evaluate business customers from your Lightspeed e-commerce platform. It intelligently scores leads (0-10), enriches company data through web research, and automatically synchronizes qualified leads to your Pipedrive CRM.

**Problem Solved:** Manual lead qualification is time-consuming and inconsistent. This system automates the entire process from order receipt to CRM entry, ensuring only high-quality B2B leads reach your sales pipeline.

## ✨ Key Features

- **Real-Time Webhook Processing** - Captures new orders instantly from Lightspeed
- **AI-Powered Lead Research** - Uses Google Gemini to research and evaluate companies
- **Intelligent Lead Scoring** - Scores leads 0-10 based on business potential
- **Duplicate Prevention** - Maintains data integrity with unique customer tracking
- **Complete Order History** - Analyzes total orders, paid orders, and revenue
- **Automated CRM Sync** - Daily batch processing to Pipedrive at 9:00 PM (CET)
- **Smart Updates** - Refreshes existing leads with new order data
- **Interactive Dashboard** - Web-based interface to monitor leads and configure settings
- **Priority Queue** - Processes highest-scoring leads first

## 🏗️ System Architecture

```
┌─────────────────┐
│   Lightspeed    │
│   E-commerce    │
└────────┬────────┘
         │ Webhook (New Order)
         ▼
┌─────────────────────────────────────────────────┐
│              n8n Workflow Engine                │
│                                                 │
│  ┌──────────────┐        ┌──────────────┐       │
│  │   Webhook    │───────▶│  Duplicate   │       │
│  │   Receiver   │        │    Check     │       │
│  └──────────────┘        └───────┬──────┘       │
│                                  │              │
│                    ┌─────────────┴─────────┐    │
│                    ▼                       ▼    │
│          ┌──────────────┐      ┌──────────────┐ │
│          │Update Existing│      │  New Lead   │ │
│          │     Lead      │      │  AI Agent   │ │
│          └──────────────┘      └───────┬──────┘ │
│                                        │        │
│                              ┌─────────▼──────┐ │
│                              │  Web Search    │ │
│                              │  AI Agent      │ │
│                              │ (Gemini API)   │ │
│                              └─────────┬──────┘ │
│                                        │        │
│                              ┌─────────▼──────┐ │
│                              │  Lead Scoring  │ │
│                              │   (Score > 5)  │ │
│                              └─────────┬──────┘ │
│                                        │        │
│                              ┌─────────▼──────┐ │
│                              │   Database     │ │
│                              │   (Queued)     │ │
│                              └────────────────┘ │
└─────────────────────────────────────────────────┘
                    │
                    │ Scheduled Trigger (9 PM Daily)
                    ▼
         ┌──────────────────┐
         │    Pipedrive     │
         │      CRM         │
         │                  │
         │ • Organization   │
         │ • Person         │
         │ • Deal           │
         │ • Note           │
         └──────────────────┘
```

## 🔧 Workflow Components

### 1. Main Lead Processing Workflow

**Purpose:** Handles incoming orders, performs AI qualification, and manages database operations.

**Flow:**
1. **Webhook Trigger** - Listens for new Lightspeed orders
2. **Business Filter** - Validates if customer is a business (B2B)
3. **Duplicate Check** - Queries database using unique Lightspeed customer ID
4. **Path Split:**
   - **Existing Customer:** Updates database and Pipedrive records
   - **New Customer:** Triggers AI research workflow

#### AI Research Sub-Process

**Base AI Agent:**
- Interprets company information from Lightspeed
- Generates natural language search queries
- Evaluates if sufficient data has been collected
- Makes final qualification decision

**Web Search AI Agent:**
- Receives queries from Base Agent
- Executes multiple web searches via Google Gemini Grounding API
- Returns summarized text chunks about the company
- Iterates until Base Agent has enough information

**Decision Logic:**
```
IF AI Decision = "NO" → Stop processing
IF AI Decision = "YES" AND Lead Score > 5 → Add to queue
ELSE → Stop processing
```

### 2. Batch Processing Workflow

**Purpose:** Pushes qualified leads to Pipedrive on a schedule.

**Trigger:** Daily at 21:00 (9:00 PM) Netherlands time

**Process:**
1. Fetches batch size limit from KVS configuration table
2. Retrieves all leads with status = "queued"
3. Sorts by lead_score (highest first)
4. Limits to configured batch size
5. Loops through each lead:
   - Creates Organization in Pipedrive
   - Creates Person (contact)
   - Creates Deal (pipeline stage 1)
   - Creates Note (AI summary + order history)
6. Updates lead status to "processed"
7. Stores Pipedrive IDs in database

### 3. Order History Sub-Workflow

**Purpose:** Analyzes complete order history from Lightspeed.

**Data Retrieved:**
- Total number of orders
- Count of paid orders
- Total revenue from paid orders (€)

**Calculation:**
```javascript
paidOrders = orders.filter(order => order.status === 'paid')
totalValue = sum(paidOrders.map(order => order.priceIncl))
totalValue = round(totalValue, 2)
```

### 4. Dashboard Workflow

**Purpose:** Provides web interface for monitoring and configuration.

**Endpoint:** `GET /verpakkingenxl`

**Features:**
- Real-time lead monitoring with filters
- Status tracking (queued/processed)
- Location and score filtering
- Sortable data table with pagination
- Lead detail modal popups
- KVS configuration editor

### 5. KVS Update Workflow

**Purpose:** Updates system configuration via dashboard.

**Endpoint:** `POST /update-kvs`

**Updates:**
- AI system prompts
- Batch size limits
- Other configuration parameters

### 6. Error Notification Workflow

**Purpose:** Global error handler that automatically sends email alerts when any workflow fails.

**Trigger:** Error Trigger (catches failures from all workflows)

**Process:**
1. **Error Trigger** - Detects when any workflow execution fails
2. **Edit Error Message** - Formats error details into styled HTML email with:
   - Workflow name that failed
   - Error message from the failed node
   - Name of the node that caused the failure
   - Direct link to the execution details
3. **Notify User** - Sends email notification via SMTP

**Email Template Features:**
- Mobile-responsive HTML design
- Professional styling with clear error highlighting
- System tag: "verpakkingenxl – Lead Processing System"
- Monospace formatting for technical details
- Direct link to view full execution in n8n

**Configuration Required:**
- SMTP credentials in n8n
- Update `fromEmail` and `toEmail` in the "Notify User" node

**Note:** This workflow acts as a safety net for the entire system, ensuring you're immediately notified of any issues in the lead processing pipeline.

### Required Credentials in n8n

Configure these in n8n's credential manager:

- **Lightspeed API** (HTTP Basic Auth)
  - Username: API Key
  - Password: API Secret
  - Base URL: `api.webshopapp.com`

- **Pipedrive API** (Query Auth)
  - Parameter: `api_token`
  - Value: Your Pipedrive API token

- **Google Gemini API**
  - API Key from Google Cloud Console

- **Google Custom Search**
  - Search Engine ID (cx)
  - API Key

- **SMTP Account** (for error notifications)
  - Host: Your SMTP server
  - Port: Usually 587 or 465
  - Username: Your email address
  - Password: Your email password or app-specific password
  - Secure: False

## 🚀 Installation & Setup

### Step 1: Import Workflows

1. Clone this repository:
```bash
git clone https://github.com/anas-farooq8/verpakkingenxl.git
cd verpakkingenxl
```

2. Import workflows into n8n:
   - Open n8n interface
   - Go to Workflows → Import from File
   - Import each JSON file from `/workflows` folder

### Step 2: Create Data Tables

Create two data tables in your n8n instance:

#### Table 1: `verpakkingenxl`

Main lead database with columns:

| Column Name | Type | Description |
|------------|------|-------------|
| lightspeed_customer_id | String | Unique customer identifier (Primary Key) |
| company_name | String | Business name |
| coc_number | String | Chamber of Commerce number |
| vat_number | String | VAT registration number |
| contact_name | String | Contact person name |
| email | String | Email address |
| phone | String | Phone number |
| address | String | Full address |
| city | String | City |
| country | String | Country |
| ai_decision | String | YES/NO |
| ai_score | Number | Lead score 0-10 |
| ai_reason | Text | AI evaluation summary |
| total_orders | Number | Total order count |
| paid_orders | Number | Paid order count |
| total_value | Number | Total revenue (€) |
| status | String | queued/processed |
| pipedrive_org_id | String | Pipedrive Organization ID |
| pipedrive_person_id | String | Pipedrive Person ID |
| pipedrive_deal_id | String | Pipedrive Deal ID |
| pipedrive_note_id | String | Pipedrive Note ID |
| created_at | DateTime | Record creation timestamp |
| updated_at | DateTime | Last update timestamp |

#### Table 2: `verpakkingenxl-KVS`

Configuration key-value store:

| Column Name | Type | Description |
|------------|------|-------------|
| key | String | Configuration key (Primary Key) |
| value | Text | Configuration value |

**Required Keys:**
- `system_prompt_base_agent` - AI prompt for base agent
- `system_prompt_web_search_agent` - AI prompt for search agent
- `total_limit` - Batch processing size (e.g., "100")

### Step 3: Configure Credentials

1. Open each workflow in n8n
2. Update credential references:
   - Lightspeed API nodes → Select your Lightspeed credential
   - Pipedrive API nodes → Select your Pipedrive credential
   - Google Gemini nodes → Select your Gemini credential
   - SMTP nodes (in Error Notification workflow) → Select your SMTP credential

3. Configure Error Notification workflow:
   - Open the "Notify-On-Error" workflow
   - Update the "Notify User" node:
     - Set `fromEmail` to your sender email address
     - Set `toEmail` to the admin/recipient email address
   - Activate the workflow

### Step 4: Setup Pipedrive Custom Fields

1. Go to Pipedrive → Settings → Data fields → Organization
2. Create custom fields and note their IDs:

| Field Name | Field Type | Example ID |
|-----------|-----------|-----------|
| Lightspeed ID | Text | 1a654f5d... |
| Total Orders | Numeric | ae01b186... |
| Paid Orders | Numeric | 0a516666... |
| Total Value | Monetary | a785a890... |
| Lead Score | Numeric | e62dba18... |
| Estimated Shipping Volume | Text | 13096dc6... |
| Logistics Type | Text | 5df1b60a... |
| CoC Number | Text | 7e89f763... |
| VAT Number | Text | c1b3f8b6... |

3. Update field IDs in workflow nodes:
   - Open "Create Organization" node
   - Replace field IDs with your actual IDs
   - Repeat for "Update Organization" node

### Step 5: Configure Pipeline Settings

1. Get your Pipedrive pipeline ID and first stage ID:
   - Go to Pipedrive → Settings → Pipelines
   - Note the pipeline ID and first stage ID

2. Update in workflow:
   - Open "Create Deal" node
   - Set `pipeline_id` and `stage_id`

### Step 6: Register Lightspeed Webhook

1. Activate the main workflow to generate webhook URL
2. Copy the webhook URL from the "Webhook" node
3. Option A: Use the "Create Webhook" helper node
   - Update URL in the node
   - Execute once manually
4. Option B: Register manually in Lightspeed backend:
   - Go to Lightspeed → API → Webhooks
   - Create new webhook for "Order Created" event
   - Paste your webhook URL

### Step 7: Initialize KVS Configuration

1. Populate the KVS table with initial values:

```sql
-- Example prompts (customize for your business)
INSERT INTO verpakkingenxl_kvs (key, value) VALUES 
('system_prompt_base_agent', 'You are a B2B lead qualification expert...'),
('system_prompt_web_search_agent', 'You are a web research specialist...'),
('total_limit', '100');
```

2. Or use the dashboard to configure via UI

### Step 8: Test the System

1. **Test Webhook:**
   - Create a test B2B order in Lightspeed
   - Check n8n execution log
   - Verify database entry

2. **Test AI Research:**
   - Ensure a new company triggers AI workflow
   - Check AI decision and score in database

3. **Test Batch Processing:**
   - Manually trigger the scheduled workflow
   - Verify leads appear in Pipedrive
   - Check all 4 records created (Org, Person, Deal, Note)

4. **Test Dashboard:**
   - Access dashboard URL
   - Verify lead data displays correctly
   - Test KVS configuration updates

5. **Test Error Notifications:**
   - Manually trigger a workflow failure (e.g., invalid credentials)
   - Verify you receive an email notification
   - Check email formatting and execution link

## ⚙️ Configuration

### AI Prompts

Customize the AI behavior by editing the system prompts in the KVS table:

**Base Agent Prompt Example:**
```
You are a B2B lead qualification expert for a packaging company. 
Analyze the provided company information and determine if they are 
a good fit for our business.

Evaluate based on:
- Company size and shipping volume potential
- Industry relevance (e-commerce, manufacturing, retail)
- Geographic location and market presence
- Legitimacy and business maturity

Provide:
1. Decision: YES or NO
2. Score: 0-10 (where 10 is highest priority)
3. Detailed reasoning for your decision
```

**Web Search Agent Prompt Example:**
```
You are a web research specialist. Given a company name and details,
search the internet to find:
- Company size and employee count
- Business model and products/services
- Shipping and logistics needs
- Market presence and reputation
- Industry and sector information

Return concise, factual information that helps evaluate the company
as a potential B2B customer for packaging supplies.
```

### Batch Processing

Adjust the number of leads processed daily:

```sql
UPDATE verpakkingenxl_kvs 
SET value = '50' 
WHERE key = 'total_limit';
```

### Scheduling

Modify the batch processing time:
1. Open the "Schedule Trigger" node
2. Change the cron expression or time
3. Save workflow

## 📊 Usage

### Monitoring Leads

Access the dashboard at: `https://your-n8n-instance.com/webhook/verpakkingenxl`

**Dashboard Features:**
- **Filters:**
  - Status: All, Queued, Processed
  - Location: Filter by city/country
  - Lead Score: Minimum score threshold

- **Lead Table:**
  - Sortable columns
  - Pagination (20 records per page)
  - Click row for detailed view

- **KVS Configuration Tab:**
  - Edit AI prompts
  - Adjust batch size
  - Save changes via POST request

## 🗂️ Data Structure

### Lead Processing States
### Pipedrive Record Structure

**Organization:**
- Name, address, contact details
- Custom fields: metrics, IDs, scores
- Linked to Person

**Person:**
- Contact name, email, phone
- Label: "B2B Contact"
- Linked to Organization

**Deal:**
- Title: "New Business Lead – [Company Name]"
- Pipeline: Stage 1
- Source: Lightspeed
- Linked to Organization and Person

**Note:**
- AI qualification summary
- Complete order history
- Lead score and reasoning
- Pinned to Deal

## 🐛 Troubleshooting

### Webhook Not Receiving Data

**Symptoms:** No executions when orders are placed

**Solutions:**
1. Verify webhook is registered in Lightspeed
2. Check workflow is activated
3. Use "Get All Webhooks" node to verify registration
4. Test with webhook URL directly using Postman

### AI Research Failing

**Symptoms:** Leads stuck in processing, no AI decision

**Solutions:**
1. Verify Google Gemini API credentials
2. Check API quota limits
3. Review system prompts for errors
4. Check n8n execution logs for API errors

### Leads Not Appearing in Pipedrive

**Symptoms:** Status shows "queued" but no CRM records

**Solutions:**
1. Verify Pipedrive API token is valid
2. Check custom field IDs match your Pipedrive setup
3. Verify pipeline and stage IDs are correct
4. Manually trigger batch workflow to check errors
5. Review Pipedrive API rate limits

### Duplicate Records in Pipedrive

**Symptoms:** Same company appears multiple times

**Solutions:**
1. Check if `lightspeed_customer_id` is being stored correctly
2. Verify duplicate check logic is working
3. Clear and rebuild database if corrupted
4. Check for multiple webhook registrations

### Dashboard Not Loading

**Symptoms:** 404 or blank page

**Solutions:**
1. Verify dashboard workflow is activated
2. Check webhook URL is correct
3. Review data table connections
4. Check browser console for JavaScript errors

### Error Notifications Not Sent

**Symptoms:** Workflows fail but no email received

**Solutions:**
1. Verify Error Notification workflow is activated
2. Check SMTP credentials are configured correctly
3. Verify `fromEmail` and `toEmail` are set in "Notify User" node
4. Check spam/junk folder for notification emails
5. Test SMTP connection with a simple email node
6. Review email server logs for delivery issues
7. Ensure firewall/network allows SMTP connections
