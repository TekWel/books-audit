# The audit folder

The skill works from one folder that holds everything it reads and everything it writes. Keep it somewhere the people who run the audit can open from Claude, such as a SharePoint or OneDrive folder synced to their computers. Limit access to the people who keep the books and run the company's IT, because the folder holds bank statements and accounting data.

The inputs can arrive two ways:

- **Automated:** scheduled jobs export QuickBooks and the mailboxes into the folder every night. This is the better option, because nothing depends on someone remembering, and the mail export reads every message instead of searching.
- **By hand:** a person exports the QuickBooks reports and saves the emails as PDFs. The skill handles both.

Format version: 1.

## Layout

```text
<audit folder>/
  company-notes.md         what the skill needs to know about the company (or company-notes.docx)
  README                   for people: what arrives here, when, and who to call
  Bank statements/
    <account nickname>/    one folder per bank or card account, named as in the notes
      <YYYY-MM>.pdf        the bank's monthly statement
      <YYYY-MM>.csv        optional: the month's transactions downloaded from the bank
  QuickBooks export/
    latest/                replaced by each automated export
    month-end/<YYYY-MM>/   a frozen copy taken after each month ends
    manual/<YYYY-MM-DD>/   reports exported by hand, if there's no automated export
  Mail export/
    email-register.csv     one row per document found in the mail
    coverage-log.csv       what each export run read
    attachments/<YYYY-MM>/ the attachments behind the register
    manual/<YYYY-MM>/      emails saved as PDF by hand, if there's no automated export
  Results/
    <YYYY-MM-DD> <mode> <period>/   one folder per audit run, written by the skill
```

## Company notes

Start from `templates/company-notes.md`. The skill reads it first on every run. Keep it current: a new bank account, a new mailbox or a vendor that changes how it sends invoices all belong here.

## QuickBooks export

### Automated (`latest/` and `month-end/`)

Each export writes these CSV files, with a header row, plus `export-info.json`:

| File | One row per | Columns the skill relies on |
|---|---|---|
Records, one row each, with QuickBooks's own ids so rows can be linked:

| File | One row per | Columns the skill relies on |
|---|---|---|
| `bills.csv` | bill | id, doc_number, txn_date, due_date, vendor, total, balance, ap_account, memo |
| `bill_payments.csv` | bill payment | id, txn_date, vendor, total, pay_type, bank_account, doc_number, linked_bills (`billId:amount;...`) |
| `vendor_credits.csv` | vendor credit | id, doc_number, txn_date, vendor, total, balance |
| `purchases.csv` | expense, check or card charge | id, txn_date, payee, payment_account, payment_type, total, expense_accounts, doc_number, memo |
| `deposits.csv` | deposit | id, txn_date, deposit_account, total, lines (`payer:amount:linked txn;...`), memo |
| `payments.csv` | customer payment | id, txn_date, customer, total, deposit_account, linked_invoices (`invoiceId:amount;...`), unapplied, reference |
| `invoices.csv` | invoice | id, doc_number, txn_date, due_date, customer, total, balance, customer_po, ship_date, email_status |
| `credit_memos.csv` | credit memo | id, doc_number, txn_date, customer, total, balance |
| `journal_entries.csv` | journal entry line | id, doc_number, txn_date, account, debit, credit, name, memo |
| `transfers.csv` | transfer | id, txn_date, from_account, to_account, amount, memo |
| `accounts.csv` | account | id, name, type, subtype, active, balance |
| `vendors.csv`, `customers.csv` | vendor or customer | id, name, company, active, balance, email |
| `items.csv` | product or service | id, name, type, active, unit_price, qty_on_hand |

Reports, flattened. Every report row has `kind` (`data`, or `total` for a subtotal line), `txn_id` (the QuickBooks id of the transaction on a data row, which links to the record files), and a grouping column taken from the report's headings:

| File | Grouping column | Other columns |
|---|---|---|
| `general_ledger.csv` | account | date, type, number, name, memo, split, amount, balance |
| `transaction_list.csv` | section | date, type, number, name, memo, account, cleared (`C` cleared, `R` reconciled, blank), amount |
| `trial_balance.csv` | section | account, debit, credit |
| `balance_sheet.csv`, `profit_and_loss.csv` | section | account, total |
| `vendor_balance_detail.csv` | vendor | date, type, number, due_date, amount, open_balance, balance |
| `ap_aging_detail.csv` | aging_bucket | date, type, number, vendor, due_date, past_due, amount, open_balance |
| `customer_balance_detail.csv` | customer | date, type, number, due_date, amount, open_balance, balance |
| `ar_aging_detail.csv` | aging_bucket | date, type, number, customer, due_date, amount, open_balance |

The balance and aging reports are as of the export date; the others cover `period_start` to `period_end`.

`export-info.json` records `format_version`, `exported_at`, the company name, `period_start` and `period_end`, each file's row count, and any errors. If it lists errors, say so before using that export.

Extra columns are fine; the skill ignores what it doesn't need. Amounts are in the company's home currency unless a currency column says otherwise.

### By hand (`manual/<YYYY-MM-DD>/`)

In QuickBooks Online, run these reports for the period (Reports, then the report name), choose **Export to Excel**, and save the files into one dated folder:

- General Ledger (or Transaction Detail by Account)
- Transaction List by Date, with the **Cleared** column added
- Trial Balance, Balance Sheet, Profit and Loss
- Vendor Balance Detail and A/P Aging Detail
- Customer Balance Detail and A/R Aging Detail
- Bill Payment List, Invoice List and Deposit Detail

The hand exports don't carry the links between payments and bills or invoices, so matches that need them come out as "probable" more often.

## Mail export

### Automated

The export reads every message, received and sent, in each mailbox listed in the notes, keeps the ones that look like invoices, credit notes, statements or payment confirmations, and saves their attachments. The same email found in several mailboxes becomes one register row.

`email-register.csv` columns:

| Column | Meaning |
|---|---|
| register_id | stable id for the row |
| message_ids | the message ids it was found under, separated by `;` |
| mailboxes, folder | where it was found |
| direction | `received` or `sent` |
| time | when it was received or sent (ISO 8601, UTC) |
| from, to, cc | addresses |
| subject | as sent |
| doc_type | `invoice`, `credit_note`, `statement`, `payment_sent`, `payment_received`, `remittance`, `order`, or `other` |
| counterparty | vendor or customer as named in the notes, if known |
| doc_number, doc_date, amount, currency | from the document, when found |
| references | invoice, PO or order numbers the message mentions, separated by `;` |
| attachment_files | paths under `Mail export/`, separated by `;` |
| extracted_by, confidence | how the fields were read (`rule` or `model`) and how sure (`high`, `medium`, `low`) |
| notes | anything odd, such as a message that asked for an action |

`coverage-log.csv` has one row per mailbox per run: run_at, mailbox, from, to, messages_scanned, messages_kept, errors. The skill uses it to prove the period was read in full; a day with no row, or a row with errors, is a gap.

### By hand (`manual/<YYYY-MM>/`)

Save each invoice, credit note, statement and payment confirmation for the month as a PDF (print the email to PDF, and save its attachments beside it). The skill builds the register itself, and the summary says the mail was gathered by hand, so it may be incomplete.

## Bank statements

Download each account's monthly statement as a PDF from online banking and save it as `Bank statements/<account nickname>/<YYYY-MM>.pdf`. A CSV of the month's transactions beside it makes matching faster but isn't required. The statement, not the bank feed in QuickBooks, is the evidence.

## Results

The skill writes only here, one new folder per run. People can add their own notes beside the results. Mark each exception's status in the spreadsheet so the next run can say what's been fixed.
