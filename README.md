<div align="center">

# QuickBooks MCP Server by Coupler.io

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Transport](https://img.shields.io/badge/Transport-Streamable_HTTP-blue.svg)](#)
[![Auth](https://img.shields.io/badge/Auth-OAuth_2.0-green.svg)](#)

Connect QuickBooks Online data to AI with the Coupler.io MCP server. Analyze revenue, expenses, profit and loss, cash flow, invoices, bills, accounts receivable, accounts payable, customers, and vendors using natural-language questions in ChatGPT, Claude, Gemini, Cursor, and other MCP-compatible AI tools. Requires a Coupler.io account.

[Landing page](https://www.coupler.io/mcp/quickbooks) · [Documentation](https://docs.coupler.io/ai/mcp) · [All Coupler.io MCP integrations](https://github.com/coupler-io)

</div>

## What you can ask

- Compare revenue and expenses with last quarter.
- Which customers have overdue invoices?
- What are our largest expense categories?
- Summarize current accounts receivable aging.
- How has operating cash flow changed over the last six months?

## How it works

This repository documents the QuickBooks integration for the Coupler.io MCP server.

1. Connect QuickBooks to Coupler.io.
2. Select your AI tool as the destination.
3. Connect your AI client to Coupler.io MCP.
4. Ask questions about your QuickBooks data in natural language.

Coupler.io sits between QuickBooks and your AI client. It holds the QuickBooks credential, imports the data on a schedule, and exposes the result as a data set the AI can query. Your AI client never calls the QuickBooks API itself.

```
  QuickBooks
      |        credential held by Coupler.io
      v
  Coupler.io          import, transform, store on a schedule
      |
      v
  MCP server          schema, SQL query execution
      |
      v
  Your AI client      your question, in plain language
```

When you ask a question, the AI reads the data set's schema, writes SQL, and Coupler.io runs that query on its own side. Only the result comes back to the AI, so a large data set does not have to fit into the model's context window.

| | |
|---|---|
| **MCP endpoint** | `https://mcp.coupler.io/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | OAuth 2.0 |
| **Query language** | SQL, executed by Coupler.io |
| **Refresh schedule** | From monthly to every 15 minutes, depending on your plan |

## Get started

*Note: You will need to set up a data flow in Coupler.io with QuickBooks as a source and the AI tool of your choice as the destination.*

### Claude

Use with Claude Web, Desktop, Chat, Cowork, or Claude Code.

**Via Web/Desktop:** Go to **Customize**->**Connectors**->**Connect your tools**, search for Coupler.io and add it.

**Via Claude Code CLI:**

```bash
claude mcp add coupler-io --transport streamable-http https://mcp.coupler.io/mcp
```

### ChatGPT

Install the [Coupler.io ChatGPT app](https://l.rw.rw/couplerio-chatgpt-app) and complete the authentication. You can also find it by searching for "Coupler.io" in the **Apps** section of **Settings**.

### Cursor

Find it on the [Cursor Directory](https://cursor.directory/mcp/coupler-io-official-remote-mcp).

### Gemini CLI

Go to the **AI integrations** -> **Gemini CLI** page in your Coupler.io account to copy the correct command (unique to each account). It will look like this:

```bash
gemini mcp add coupler --transport=http https://mcp.coupler.io/mcp/xxxxx
```

### OpenClaw

Use the **mcporter** skill to connect, or install the **coupler-io** skill from ClawHub.
Directly ask your OpenClaw agent to add the skill and execute it.

## Data you can access

Access entity data (invoices, customers, bills, payments, and more) and pre-built financial reports (P&amp;L, Balance Sheet, General Ledger, aging reports) from QuickBooks Online.

<details>
<summary><strong>Available entities</strong></summary>

| Entity | Description | Typical use case |
|---|---|---|
| **Invoice** | Customer invoices with line items | Revenue tracking, accounts receivable |
| **Customer** | Customer records and contact info | Customer lists, contact management |
| **Bill** | Vendor bills (accounts payable) | Expense tracking, AP aging |
| **Payment** | Customer payments received | Cash flow tracking |
| **Vendor** | Vendor/supplier records | Vendor management, AP reporting |
| **Employee** | Employee records | Payroll, HR reporting |
| **Estimate** | Quotes and estimates | Sales pipeline tracking |
| **Purchase** | Purchases and expenses | Expense analysis |
| **PurchaseOrder** | Purchase orders | Procurement tracking |
| **SalesReceipt** | Point-of-sale receipts | Retail and cash sales |
| **CreditMemo** | Credit memos issued | Refund and credit tracking |
| **Deposit** | Bank deposits | Cash flow, deposit reconciliation |
| **Transfer** | Bank-to-bank transfers | Cash management |
| **JournalEntry** | Manual journal entries | Adjustments, accruals |
| **Account** | Chart of accounts | Account structure and balances |
| **Item** | Products and services | Inventory, catalog management |
| **Budget** | Budget records | Budget vs. actual analysis |
| **TimeActivity** | Time tracking entries | Billable hours, payroll hours |

</details>

<details>
<summary><strong>Financial reports</strong></summary>

#### Summary reports

| Report | What it shows | Key parameters |
|---|---|---|
| **Profit and Loss Summary** | Revenue and expenses by account | `accounting_method`, `class`, `department` |
| **Balance Sheet** | Assets, liabilities, and equity snapshot | `accounting_method`, `adjusted_gain_loss` |
| **Cash Flow** | Cash inflows and outflows | `class`, `department`, `customer` |
| **Trial Balance** | Debit/credit balances for all accounts | `accounting_method` |
| **Expenses by Vendor** | Expense totals grouped by vendor | `accounting_method`, `class` |
| **Sales by Customer** | Sales totals grouped by customer | `accounting_method`, `class` |
| **Sales by Product** | Sales totals grouped by product/service | `accounting_method`, `department` |
| **Sales by Class Summary** | Sales totals grouped by class | `accounting_method` |
| **Sales by Department** | Sales totals grouped by department/location | `accounting_method` |
| **Tax Summary** | Tax collected and owed | — |
| **Inventory Valuation Summary** | Inventory quantities and values | — |

#### Detail reports

| Report | What it shows | Key columns |
|---|---|---|
| **Profit and Loss Detail** | Individual transactions behind P&L line items | Date, Type, Name, Amount, Balance |
| **General Ledger Detail** | All transactions by account with running balance | Date, Account, Debit, Credit, Balance |
| **Transaction List** | All transactions in a flat list | Date, Type, Account, Amount |
| **Transaction List by Customer** | Transactions grouped by customer | Date, Type, Customer, Amount |
| **Transaction List by Vendor** | Transactions grouped by vendor | Date, Type, Vendor/Supplier, Amount |
| **Transaction List with Splits** | Transactions showing all split lines | Date, Account, Amount, Product/Service |
| **Journal Report** | Journal entries with debit/credit detail | Date, Account, Debit, Credit |

#### Aging and balance reports

| Report | What it shows |
|---|---|
| **AP Aging Detail / Summary** | Outstanding vendor bills by aging period |
| **AR Aging Detail / Summary** | Outstanding customer invoices by aging period |
| **Customer Balance / Detail** | Customer balances and underlying transactions |
| **Vendor Balance / Detail** | Vendor balances and underlying transactions |
| **Customer Income** | Income by customer |
| **Account List Detail** | Chart of accounts with balances |

</details>

Coupler.io imports reports with the parameters set on the source: accounting method, class, department, and date range among them. Changing those parameters changes the numbers, so keep them consistent when comparing periods.

## Example questions

### Profit and loss

- Compare revenue and expenses with last quarter.
- What are our largest expense categories this year?
- What changed in the P&L this month versus last month?

### Receivables and payables

- Which customers have overdue invoices?
- Summarize current accounts receivable aging.
- Which vendor bills are coming due in the next 30 days?

### Cash and customers

- How has operating cash flow changed over the last six months?
- Which customers generate the most income?
- Compare actual spend against budget by account.

## Security and permissions

Your AI client never connects to QuickBooks directly. Coupler.io holds the QuickBooks credential, imports the data, and exposes only the resulting data set over MCP.

- **Your QuickBooks data is never modified.** Coupler.io only reads from QuickBooks. The AI queries the copy Coupler.io imported and cannot edit, delete, or overwrite it, let alone write anything back to your QuickBooks account.
- **Visibility is scoped per AI tool.** An AI client sees only the data sets from data flows that have *that client* set as a destination. Adding Claude as a destination does not expose the data flow to ChatGPT, though one flow can name both.
- **Configuration changes are possible, and confirmed first.** With the full tool set available, the AI can create data flows, add sources and destinations, change a schedule, or trigger a run. Those are real changes to your workspace, so the server instructs the AI to confirm before making one you did not ask for.
- **Nothing else is reachable.** The MCP server exposes the data sets described above and nothing more. It cannot reach your other accounts or your machine.
- **Disconnect at any time** by removing the connector in your AI client, or by deleting the credential or the data flow in Coupler.io.

Coupler.io is SOC 2 certified and compliant with GDPR and HIPAA.

## Troubleshooting

**The AI cannot find my QuickBooks data set.**
Usually you have not added that AI tool as a destination yet. Open the data flow in Coupler.io and add your AI client. One data flow can have several AI tools as destinations at the same time, so adding ChatGPT does not displace Claude. Each tool sees only the flows it is named on.

**The numbers look out of date.**
The AI reads the last imported snapshot, not QuickBooks live. Check the data flow's refresh schedule, or ask your AI client to run the data flow now.

**A field I need is missing.**
Coupler.io imports only the fields you select in the data flow's source. Add the missing fields and re-run the flow.

**The AI misreads a metric.**
Save the business context on the data set: what a metric means, which currency it is in, which rows to exclude. You do not have to leave your AI tool to do it, just tell the assistant to update the data set context and it saves it for you. The AI reads that context before it queries, so the next conversation uses your definitions instead of guessing.

**The connector does not appear in my AI client.**
Availability differs by AI client and subscription plan. Follow the client-specific steps under [Get started](#get-started), and check the [AI destination docs](https://docs.coupler.io/destinations/categories/ai) for that tool.

## Related Coupler.io MCP integrations

- [Shopify MCP](https://github.com/coupler-io/shopify-mcp) — connect ecommerce sales with accounting and financial data
- [Google BigQuery MCP](https://github.com/coupler-io/google-bigquery-mcp) — combine financial data with other business datasets
- [HubSpot MCP](https://github.com/coupler-io/hubspot-mcp) — connect sales pipeline and customer data with financial performance

[Explore all Coupler.io MCP integrations](https://github.com/coupler-io)

## FAQ

### What is the QuickBooks MCP server?

It is the QuickBooks integration for the Coupler.io MCP server, an endpoint that lets AI clients query your QuickBooks data in plain language. Coupler.io imports the data, stores it, and answers the AI's SQL queries on its own infrastructure.

### Do I need a Coupler.io account?

Yes. The MCP server serves data from your Coupler.io workspace, so you need an account with a data flow that has QuickBooks as a source and your AI tool as a destination.

### Does this connect directly to my QuickBooks account?

No. Coupler.io connects to QuickBooks, imports the data, and exposes the resulting data set over MCP. Your AI client talks to Coupler.io, never to QuickBooks.

### Which QuickBooks data can AI access?

Whatever your data flow imports. See [Data you can access](#data-you-can-access) for the full catalog of report types and fields. The AI reaches only the data sets in flows that name your AI tool as a destination.

### Is the integration read-only?

Yes. Nothing you or your AI client does through Coupler.io changes your QuickBooks data. Coupler.io only reads from QuickBooks, and the AI only queries the copy Coupler.io imported. It cannot edit, delete, or write anything back to your QuickBooks account.

### Which AI assistants can I use?

Claude, ChatGPT, Cursor, Gemini CLI, OpenClaw, Perplexity, and any client that speaks MCP through the Custom MCP destination. Setup steps for the clients above are under [Get started](#get-started); for the rest, see the [AI destination docs](https://docs.coupler.io/destinations/categories/ai).

### Do I need to write SQL or code?

No. You ask in plain language; the AI writes the SQL and Coupler.io runs it. Writing SQL yourself stays an option if you want a specific transformation.

### How fresh is the data?

As fresh as the last data flow run. Schedules range from monthly to every 15 minutes depending on your plan, and you can ask your AI client to refresh the flow on demand.

## Links

- **Landing page:** [QuickBooks MCP by Coupler.io](https://www.coupler.io/mcp/quickbooks)
- **Documentation:** [Coupler.io MCP](https://docs.coupler.io/ai/mcp)
- **Coupler.io:** [https://coupler.io](https://coupler.io)
- **MCP Server endpoint:** `https://mcp.coupler.io/mcp`
- **All Coupler.io MCP integrations:** [https://github.com/coupler-io](https://github.com/coupler-io)
