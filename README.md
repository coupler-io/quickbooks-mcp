<div align="center">

# QuickBooks MCP Server by Coupler.io

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Transport](https://img.shields.io/badge/Transport-Streamable_HTTP-blue.svg)](#)
[![Auth](https://img.shields.io/badge/Auth-OAuth_2.0-green.svg)](#)

Coupler.io QuickBooks MCP server for Claude, ChatGPT, Gemini, Cursor, n8n, OpenClaw, and other MCP clients. Query and analyze QuickBooks data with natural language. Requires the Coupler.io account.

</div>

## Data Access

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


## Supported Clients

*Note: You will need to set up a data flow in Coupler.io with QuickBooks as a source and the AI tool of your choice as the destination.*

### Claude

Use with Claude Web, Desktop, Chat, Cowork, or Claude Code.

**Via Web/Desktop:** Go to **Customize**->**Connectors**->**Connect your tools**, search for Coupler.io and add it.

**Via Claude Code CLI:**

```bash
claude mcp add coupler-io --transport streamable-http https://mcp.coupler.io/mcp
```

### ChatGPT

Install from the **ChatGPT Apps** directory — search for "Coupler.io" in the **Apps** section of **Settings**.

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

## Links

- **Landing page:** [QuickBooks MCP by Coupler.io](https://www.coupler.io/mcp/quickbooks)
- **Coupler.io:** [https://coupler.io](https://coupler.io)
- **MCP Server endpoint:** `https://mcp.coupler.io/mcp`