# Automated Lead Processing & Enrichment System

> An intelligent B2B lead qualification system built with n8n that automatically captures, researches, scores, and syncs qualified business leads from Lightspeed to Pipedrive CRM.

![n8n](https://img.shields.io/badge/n8n-Workflow-EA4B71?logo=n8n)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI-4285F4?logo=google)
![Gmail](https://img.shields.io/badge/Gmail-API-EA4335?logo=gmail)

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

## 🙏 Acknowledgments
