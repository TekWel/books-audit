# books-audit

A Claude plugin that audits a small business's books. It compares QuickBooks Online exports, bank statements, and the invoices and payment confirmations in email, then lists every place they disagree, with the evidence for each, for a person to fix.

It reads and reports. It never changes QuickBooks, email or the bank, and it writes only to a `Results` folder.

## What it checks

1. Vendor invoices and credits in the email against QuickBooks bills
2. Payments out: bank, QuickBooks and payment confirmations
3. Payments in: customer payment notices, bank deposits and QuickBooks payments
4. Customer invoices sent by email against QuickBooks invoices
5. Each vendor statement's balance against QuickBooks, explained to the cent
6. Each bank statement's balance against the QuickBooks register

Every run produces `exceptions.xlsx` (one row per problem, with evidence and a suggested fix) and a one-page `summary.md`.

## Install

**Claude desktop app (Cowork):** Customize, then Plugins, then add a marketplace from a repository: `TekWel/books-audit`. Install **books-audit** from it. To get a newer version later, check the marketplace for updates.

**Claude Code:**

```text
/plugin marketplace add TekWel/books-audit
/plugin install books-audit@books-audit
```

## Set up the audit folder

The skill works from one folder holding the company notes, the QuickBooks export, the mail export, the bank statements and the results. The layout, the file formats, and how to fill it automatically or by hand are in [folder-setup.md](plugins/books-audit/skills/books-audit/references/folder-setup.md). Start the company notes from [the template](plugins/books-audit/skills/books-audit/templates/company-notes.md).

Keep the folder limited to the people who keep the books and run IT. It holds bank statements and accounting data.

## Use

Open Claude in the audit folder and ask, for example:

- "Run the books audit for October."
- "Catch-up audit from March 2025 to October 2026."
- "Explain the difference between this vendor's statement and QuickBooks."

The skill reads the company notes, checks the inputs cover the period, runs the checks, rechecks every exception against its source, and saves the results in a new dated folder.

## Limits

- It doesn't post corrections or reconcile accounts inside QuickBooks; a person does that from the results.
- It doesn't decide how something should be booked. Those come back as questions for the bookkeeper.
- It isn't tax, legal or accounting advice.
