# Setup wizard

Use this whenever something the audit needs is missing: no folder connected, no company notes, or inputs missing for the period. It is also the whole job when the person asks to set up the books audit.

## How to run it

- **One step at a time.** Start each message with "Step N of 6", say in one sentence what the step is for, give the person something specific to do or a short set of choices, and stop. Wait for the answer before moving on.
- **Skip what's already done.** Check the folder first, mark finished steps as done in a one-line progress list, and start at the first unfinished step.
- **Do the work for them where you can.** Create folders, write the company notes from their answers, and draft the folder's README. Ask before creating anything, and never move, rename or delete their files without an explicit yes for that file.
- **Never search their computer.** Look only inside folders the person connects or names. If you can't find something, ask where it is.
- **Plain words.** No file formats or jargon unless they ask. Say "your QuickBooks reports", not "the CSV export".
- **Never ask for full account numbers, passwords or sign-in details.** Last four digits are enough.

Progress line, at the top of each step after the first:

```text
Done: folder, notes   Now: QuickBooks   Next: mail, bank statements, first run
```

## Step 1 of 6: the folder

Explain: the audit keeps everything in one folder, so it can show its evidence and save its results.

Ask which fits:

1. **"We already have a books audit folder."** Ask them to connect it. In the Claude desktop app that's the folder button where they start a task; in Claude Code it's opening Claude in that folder. Once it's connected, check it against the layout in `folder-setup.md`.
2. **"It's in SharePoint or OneDrive."** Syncing is the best way, because the audit then reads every file directly and its results land back in SharePoint on their own. Walk them through it one action at a time:
   1. Open the folder in SharePoint in the browser.
   2. Click **Sync** (or **Add shortcut to My files**, then open OneDrive on the computer).
   3. Wait until the folder shows up in File Explorer or Finder, usually under the company's name.
   4. Connect that local folder in Claude.

   If they can't sync (for example, on a computer without OneDrive) and a Microsoft 365 or SharePoint connector is connected in Claude, offer to work from SharePoint through the connector instead:
   - It's read-only, and reading through a connector is slower for a full month of files.
   - The results can't be saved back to SharePoint that way. Save them in a local folder they connect, and ask them to upload that folder into `Results`.
   - Say so in the summary.
3. **"Start a new one."** Ask where it should live. Suggest a shared, synced location over a personal folder, because it holds bank statements and accounting data and others may need it. Once they've connected the empty folder, create the layout from `folder-setup.md`.

If the connected folder is missing some subfolders, list them and offer to create them.

## Step 2 of 6: company notes

Explain: these notes tell the audit which accounts, mailboxes, vendors and customers to look at. They're written once and updated when something changes.

If `company-notes.md` (or `.docx`) exists, read it, show a short summary, and ask only about empty or unclear sections.

If it doesn't exist, build it from `templates/company-notes.md` by asking in small groups, one group per message:

1. Company name as it appears in QuickBooks, the bookkeeper, and the smallest amount worth flagging (suggest $5.00).
2. Bank and card accounts: a nickname, the bank, the last four digits, and the account's name in QuickBooks.
   - If a QuickBooks export is already in the folder, list the bank and card accounts from it and ask them to confirm instead.
3. The mailboxes where invoices and payment confirmations arrive.
4. The vendors that matter most, with the email address or domain each sends from, and whether they send statements.
   - If an export is there, offer the vendors with the most bills as a starting list.
5. Customers who pay by bank transfer, and who sends their remittances.
6. Known problems they already know about, and anything to skip.

Write the notes, show them, and ask "Anything to change?" before saving the final version.

## Step 3 of 6: QuickBooks

Explain: the audit compares everything against QuickBooks, so it needs QuickBooks's records for the period.

- If `QuickBooks export/latest/` exists, check `export-info.json`: when it was taken and which dates it covers. If it's fresh and covers the period, mark the step done.
- If not, ask whether someone set up an automatic export:
  - **Yes, but it's missing or old:** tell them to ask whoever runs it, and offer to continue with a by-hand export in the meantime.
  - **No:** walk them through the by-hand export in `folder-setup.md`, **one report per message**. Give the report name, the date range, the **Export to Excel** button, and the folder to save it in (`QuickBooks export/manual/<today>/`). Confirm each file arrived before giving the next report.

## Step 4 of 6: mail

Explain: invoices and payment confirmations arrive by email, and the audit checks each one against QuickBooks and the bank.

- If `Mail export/` has a register and a coverage log covering the period, mark the step done.
- If not, offer the choices that apply:
  1. **An automatic export is being set up.** Continue with the other steps, and note that the mail checks wait for it.
  2. **A mail connector is connected in Claude** (for example Microsoft 365 or Gmail). Offer to search the mailboxes in the notes, read-only, for the period, and build the register from what it finds. Say plainly that a search can miss messages an export would catch, and note this in the results.
  3. **By hand.** For each mailbox, have them save that month's invoices, credit notes, statements and payment confirmations as PDFs into `Mail export/manual/<YYYY-MM>/`. Give them the senders from the notes to search for.

## Step 5 of 6: bank statements

Explain: the bank statement is the proof of what money actually moved.

List what's there and what's missing as a table, with one row per account from the notes and one column per month in the period. For each missing statement, give the exact place to save it: `Bank statements/<nickname>/<YYYY-MM>.pdf`. Ask them to download each one from online banking and say "done" when they're in.

If a statement arrives with a different name, ask before renaming it to the layout.

## Step 6 of 6: first run

Show a checklist of everything in place, with gaps marked:

```text
Folder            ready
Company notes     ready
QuickBooks        exported Nov 16, covers Oct 1 to Oct 31
Mail              2 mailboxes, every day of October, no errors
Bank statements   2 of 2 accounts for October
```

Draft the folder's `README` from `templates/folder-readme.md` if it doesn't have one, and ask before saving it.

Then offer to run the audit for the period. For a first run, suggest one recent month, even if they plan a catch-up later. It's quicker, and it shows them what the results look like. If something is still missing, say which checks will be skipped or weaker because of it, and ask whether to go ahead.
