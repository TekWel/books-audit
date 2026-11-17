# Outputs

Write everything into a new folder, `Results/<YYYY-MM-DD> <monthly|catch-up> <period>/`. Use today's date and a period such as `2026-10` or `2025-03 to 2026-10`.

## exceptions.xlsx

### Sheet "Exceptions": one row per problem

| Column | What goes in it |
|---|---|
| id | E001, E002, ... in the order found |
| check | 1 to 6, from `checks.md` |
| type | missing bill, duplicate bill, amount differs, credit not entered, bill without document, payment not in QuickBooks, payment not in bank, booked to cost instead of applied, paid twice, deposit not applied, confirmation without payment, deposit not recorded, payment not deposited, applied to wrong invoice, invoice open after payment, payment promised not received, invoice missing in QuickBooks, statement difference, bank difference, uncleared item, never reconciled, possible duplicate account, other |
| counterparty | vendor, customer or payee |
| date | the document or transaction date |
| amount | the amount at issue |
| document | the number, and where it is: file and page, or the email's date, sender and subject |
| quickbooks | the record type, number, date and amount, or "none" |
| bank | account (last four digits), date and amount, or "none" |
| difference | the gap in money, when there is one |
| suggested fix | what a person should probably do in QuickBooks, in one line |
| match | exact, probable or none |
| confidence | high, medium or low |
| rechecked | yes, once the second look holds |
| status | left blank for the person: open, fixed, not an issue |
| notes | anything else |

### Other sheets

- **"Vendor tie-outs":** one table per vendor statement. The statement balance, each reconciling item with evidence, the QuickBooks balance, and anything unexplained.
- **"Bank tie-outs":** the same for each bank account.
- **"Unconfirmed":** items that look wrong but have no document yet, with what's needed to confirm them.
- **"Email register":** the register rows for the period that the audit used.

If a previous run's `exceptions.xlsx` exists, carry its status column over for the same problems, and mark which earlier problems are now gone.

## summary.md

Keep it to about a page:

1. **Period and mode.**
2. **Inputs used and gaps:** export dates; mail coverage per mailbox (messages read and kept); statements present; anything missing.
3. **Headline:** the number of exceptions and the money involved, by type.
4. **Tie-outs:** the vendor and bank tables in short form, each ending in "explained to the cent" or the unexplained amount.
5. **Fix first:** the 5 to 10 items that matter most, by money and by risk (paying twice, money not received, bills missing).
6. **Unconfirmed items** and what would confirm them.
7. **Questions for the bookkeeper,** including any booking decision the audit can't make.
8. **Anything in the mail that asked for an action,** such as changed bank details. It was not acted on.

Use plain words, give every money amount to the cent, and leave out full account numbers.
