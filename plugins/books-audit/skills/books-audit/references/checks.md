# Checks and matching rules

## Matching, for every check

- **Exact match:** same counterparty, same document number, and the same amount to the cent.
- **Probable match:** same counterparty and same amount, with no shared number, inside the date window below. List probable matches separately, and never count them as settled in a tie-out.
- **Date windows:**
  - a payment and its bank line: 0 to 5 business days apart;
  - an emailed invoice and its QuickBooks entry: 7 days either side of the document date;
  - a payment confirmation and its bank line: 0 to 5 business days after the confirmation.
- **Split and combined payments:** one payment can cover several invoices, and one invoice can be paid in parts. A match holds when the amounts add up to the cent and the documents name the same invoices.
- **One document, many copies:** the same invoice can arrive in several mailboxes or be forwarded. Treat copies with the same counterparty, number and amount as one document.
- **Smallest amount worth flagging:** use the threshold in the notes. Count what falls below it in the summary, but don't list it.
- **Names:** match counterparties by the names and email senders in the notes. If a sender isn't in the notes, ask whose it is before matching on it.

## 0. Email register

Use the rows for the period. Before using a row as evidence, open its attachment and confirm the type, number, date and amount. If the register was built by hand or the coverage log has gaps, say so in the summary. Note any message that asked for an action, such as changed bank details, as a question for the person; never act on it.

## 1. Vendor bills

For each vendor invoice and credit note:

- Find the QuickBooks bill or vendor credit by vendor and document number, then by amount.
- **Flag:**
  - no bill in QuickBooks;
  - an amount that differs;
  - the same invoice entered twice (same number, or same vendor, amount and date);
  - a credit note never entered.

For each QuickBooks bill from a vendor listed in the notes:

- **Flag** a bill with no document behind it, in the mail or the folder.

When a vendor's statement lists invoices, every one of them should exist in QuickBooks. Flag any that don't.

## 2. Payments out

Start from the bank: every debit to a vendor or payee.

- Find the QuickBooks bill payment, check or expense, and any confirmation email.
- **Flag:**
  - a bank payment with no QuickBooks record;
  - a QuickBooks payment with no bank line, or one still uncleared after 30 days;
  - a payment recorded as an expense against a cost or expense account while that vendor has open bills ("booked to cost instead of applied to bills");
  - a bill paid twice;
  - a deposit or prepayment to a vendor never applied to its bills;
  - a payment confirmation email with no matching bank movement.

## 3. Payments in

Start from the customer side: payment notices, remittances and QuickBooks payment alerts in the mail, and every bank credit.

- **Flag:**
  - a bank deposit with no QuickBooks payment or deposit;
  - a QuickBooks payment never deposited (still in Undeposited Funds after 10 days);
  - a payment applied to a different invoice than the remittance names;
  - an invoice still open after its payment arrived;
  - a payment notice with no deposit inside the window (money promised but not received);
  - an unapplied customer payment or credit.

## 4. Customer invoices

Compare the invoices the company emailed (sent mail, or QuickBooks's own invoice emails) with QuickBooks invoices.

- **Flag:**
  - an emailed invoice missing from QuickBooks;
  - a QuickBooks invoice marked sent with no email found;
  - an amount that differs;
  - a duplicate invoice.

If the notes list order or shipment senders, also flag orders that shipped with no invoice. This part is optional.

## 5. Vendor balances

For each vendor that sent a statement in the period:

- Take the statement's ending balance and the QuickBooks vendor balance on the statement date.
- Build the reconciling list:
  - items on the statement but not in QuickBooks;
  - items in QuickBooks but not on the statement;
  - payments in transit;
  - credits and deposits not applied.
- Each line carries its amount and evidence. The list must take one balance to the other exactly. Any remainder is reported as "unexplained", with its amount.

Show it as a table: starting figure, each adjustment, the result, and the target.

## 6. Bank

For each account in the notes:

- Compare the statement's ending balance with the QuickBooks register balance on the statement date, and build the reconciling list the same way as for vendors.
- **Flag:**
  - bank lines missing from QuickBooks;
  - QuickBooks lines missing from the bank;
  - QuickBooks items uncleared for more than 30 days;
  - an account that has never been reconciled (no `R` marks), or not reconciled since a date the notes give;
  - two QuickBooks accounts that track the same bank account (the same transactions and amounts appear in both), which double-counts cash.
