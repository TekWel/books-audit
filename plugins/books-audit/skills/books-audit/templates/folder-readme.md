# Books audit folder

This folder holds what Claude's books audit reads and what it writes. Open Claude in this folder and ask, for example, "run the books audit for October".

## What's here

| Folder | What goes in it | How it gets there |
|---|---|---|
| company-notes | Accounts, mailboxes, vendors and customers the audit checks | Written during setup; update it when something changes |
| Bank statements | One PDF per account per month, `<YYYY-MM>.pdf` | Downloaded from online banking each month by: |
| QuickBooks export | QuickBooks records and reports | Automatic every night, or exported by hand into `manual` |
| Mail export | The invoices and payment confirmations found in email | Automatic every night, or saved by hand into `manual` |
| Results | One folder per audit run: the problems found and a summary | Written by the audit |

## Who to ask

- Missing or old exports:
- Questions about the results:

## Rules

- The audit only reads. It never changes QuickBooks, email or the bank.
- Keep this folder limited to the people who keep the books and run IT.
- Mark each problem's status in the results spreadsheet (open, fixed, not an issue) so the next run knows what's been dealt with.
