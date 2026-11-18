# Setup wizard

Use this whenever something the audit needs is missing: no folder connected, no company notes, or inputs missing for the period. It is also the whole job when the person asks to set up the books audit.

The goal is to be ready to run in as few messages as possible. When scheduled exports already fill the folder and the notes are written, that's two or three messages: connect the folder, see the checklist, add the bank statements, run.

## How to run it

- **Check everything first.** As soon as a folder is connected, check every input in one pass and show one checklist (below). Only the gaps need the person; don't walk them through anything that's already in place.
- **Draft, then ask.** Fill in what you can from what's already in the folder: bank and card accounts and vendors from the QuickBooks export, mailboxes and senders from the email register. Ask the person to correct the draft rather than answer open questions.
- **Batch.** Put everything the person has to do in one message as a numbered list, and ask all your questions together. Stop only when you need their answer or their files to go on.
- **Keep it short.** At most one sentence of why, and only for something they have to do. No step numbers or progress lines.
- **Do the work for them.** Create missing subfolders, write the notes and the README. Ask once before saving, in the same message as your next question.
- **Never search their computer.** Look only inside folders the person connects or names. If you can't find something, ask where it is.
- **Plain words.** Say "your QuickBooks reports", not "the CSV export".
- **Never ask for full account numbers, passwords or sign-in details.** Last four digits are enough.

## 1. Connect the folder

Skip this if a folder is connected. Otherwise, in one message, ask for the folder's SharePoint or OneDrive link and give the sync steps for their computer (tell Windows from Mac from what you can see; if you can't tell, give both):

1. Open the link and sign in with the work account.
2. Click **Add shortcut to My files** in the toolbar (or the folder's **...** menu). This syncs just that folder, which is usually what they want. **Sync** syncs the whole library instead.
3. Find it on the computer. The first sync can take a few minutes.
   - **Windows:** File Explorer, under **OneDrive - <company>**.
   - **Mac:** with the OneDrive app installed and signed in, Finder's sidebar under **OneDrive - <company>**.
   - Not there? Click the OneDrive cloud icon (taskbar or menu bar) and check it's signed in and syncing.
4. Connect that folder in Claude (the folder button where they start a task) and say "done".

When it's connected, check the path is inside OneDrive or the company's synced folder. If it's somewhere like Downloads or the desktop, it's probably a copy whose results won't reach anyone else: say so, and give the steps again.

Other cases:

- **They already have the folder on this computer:** have them connect it.
- **They don't have one yet:** suggest making it in SharePoint, limited to the people who keep the books and run IT, since it holds bank statements and accounting data. Then sync it as above, and create the layout from `folder-setup.md` once it's connected.
- **They can't sync on this computer,** and a Microsoft 365 or SharePoint connector is connected in Claude: offer to read the folder through the connector. It's read-only and slower, and results can't go back to SharePoint that way: save them to a local folder they connect, and ask them to upload it into `Results`. Say so in the summary.

## 2. Check everything and show the checklist

Check, for the period (default: the last full month):

- **Folder:** the layout in `folder-setup.md`. Create missing subfolders (they're empty) and say so in the checklist.
- **Company notes:** `company-notes.md` or `.docx` exists and its tables aren't empty.
- **QuickBooks:** `QuickBooks export/latest/export-info.json`: when it was taken, the dates it covers, and any errors. Otherwise `manual/`.
- **Mail:** `Mail export/email-register.csv` and `coverage-log.csv`: every day of the period read without errors for each mailbox. Otherwise `manual/`.
- **Bank statements:** one per account in the notes per month.
- **README:** at the folder's top level.

Show one checklist, then in the same message deal with every gap as below:

```text
Folder            ready
Company notes     missing: draft below
QuickBooks        exported Nov 16, 1:30 AM, covers Jan 1, 2025 to Nov 16
Mail              2 mailboxes, every day of October, no errors
Bank statements   October: 1 of 2 (missing: Operating)
README            missing: I'll write it with the notes
```

If nothing is missing, offer to run the audit right away.

## 3. Fill the gaps

### Company notes

If they exist, read them and ask only about empty or unclear sections. Don't recite them back.

If they're missing, draft them from `templates/company-notes.md` using the folder:

- Bank and card accounts from the QuickBooks export's `accounts.csv` (Bank and Credit Card types), with the last four digits when the account name shows them.
- Mailboxes from the coverage log.
- Vendors with the most bills, and their senders from the email register.

Show the draft and, in the same message, ask what the folder can't tell you:

1. Is anything in the draft wrong or missing?
2. Who keeps the books, and who answers booking questions?
3. The smallest amount worth flagging (suggest $5.00).
4. Problems they already know about, and anything to skip.

Save the notes when they say it's right.

### QuickBooks

- **A fresh export covering the period:** nothing to do.
- **The scheduled export is missing or old:** tell them to ask whoever runs it (the README names them), and offer the by-hand export meanwhile.
- **By hand:** in one message, list every report in `folder-setup.md` with the date range, the **Export to Excel** button, and the folder (`QuickBooks export/manual/<today>/`). When they say done, check them all at once and name only what's missing.

### Mail

- **A register and coverage log covering the period:** nothing to do.
- Otherwise, offer the choices that apply, one line each:
  1. **A scheduled export is being set up:** go ahead, and the mail checks wait for it.
  2. **A mail connector is connected** (Microsoft 365, Gmail): search the mailboxes in the notes, read-only, and build the register from what you find. A search can miss messages an export would catch; say so in the results.
  3. **By hand:** save the month's invoices, credit notes, statements and payment confirmations as PDFs into `Mail export/manual/<YYYY-MM>/`. Give them the senders from the notes to search for.

### Bank statements

Show one table, one row per account and one column per month, and give the exact place for each missing statement: `Bank statements/<nickname>/<YYYY-MM>.pdf`. Ask them to download them from online banking and say "done". If a file arrives with another name, ask before renaming it.

If statements are the only gap, offer to start now: everything except the bank checks can run, and those run when the statements arrive.

### README

If there's none, draft it from `templates/folder-readme.md` and save it with the same yes as the notes.

## 4. Run

When nothing blocks, offer the run in the same message as the checklist. For a first run, suggest one recent month, even if they plan a catch-up later; it's quicker and shows them what the results look like. If something is still missing, say which checks will be skipped or weaker, and ask whether to go ahead.
