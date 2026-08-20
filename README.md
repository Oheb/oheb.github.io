# Analytics Bud — Customer Success User Guide

---

## 1. What Is Analytics Bud?

Analytics Bud is a Slack app that runs campaign reports for you and posts the results back into Slack.

Instead of asking an analyst to pull numbers, you fill out a short form in Slack, pick your campaign and date range, and Analytics Bud runs the report and posts a summary — impressions, clicks, spend, CTR, CPA, top sites, top states, and so on — directly in the conversation. You can then share that message with a colleague or a channel, or download the full results as a spreadsheet file (CSV).

**Use Analytics Bud when you need:**

- Delivery and performance numbers for a campaign over a date range
- A breakdown by geography, site/app, creative, line item, tactic, day, device, or frequency
- A quick, shareable answer in Slack for a client question
- A CSV you can open in Excel and send to a client

**Analytics Bud is not the right tool when:**

- You need a very long date range (see Section 4)
- You need row-level lists of individual users — Analytics Bud reports counts and summaries, not user lists
- You need a custom calculation that isn't one of the built-in reports

Most reports finish in roughly **5 to 15 minutes**. Long date ranges, lots of selected metrics, and multiple breakdowns all push that higher — see Section 6 for how to keep reports fast.

---

## 2. Before You Start

### You must be connected to the Cisco VPN

Analytics Bud reads from an internal reporting system that is only reachable over the company network. **If you are not connected to the Cisco VPN, your reports will fail.**

Connect Cisco AnyConnect (ZetaGlobal US-EAST) before you run anything.

### Analytics Bud only understands slash commands — it is not a chatbot

**Every interaction with Analytics Bud happens through a slash command** — a message that starts with `/`, like `/form-report` or `/analytics-bud status`. This is true everywhere, **including inside the Analytics Bud app itself.** When you open Analytics Bud from your Slack sidebar and land in its Messages tab, that looks like a normal chat window, but it is not one.

There is **no natural language conversation** with Analytics Bud. Typing things like:

- *"run me a geography report for campaign 231369"*
- *"is my report done yet?"*
- *"hey can you export that"*

will not do anything. Analytics Bud will not reply, will not ask a follow-up question, and will not interpret what you meant.

The correct approach, in the Analytics Bud app or anywhere else in Slack, is always:

```text
/form-report
```

…and then use the form. Treat the Analytics Bud Messages tab as a place where the app **posts things to you**, not a place where you talk to it.

### Check that Analytics Bud can reach the reporting system

Run this from anywhere in Slack:

```text
/analytics-bud ping
```

You'll get one of two answers:

- **"Hive MCP is connected"** — you're good to go. ("Hive" is the name of the reporting system where your report runs; you'll see this word in some Analytics Bud messages.)
- **"Hive MCP is not reachable"** — do not submit a report yet. Check your VPN first. If VPN is connected and it still fails, see Section 13 (escalation).

### Have your campaign details ready

Before opening the form, know:

- The **campaign ID** (numeric, e.g. `231369`) — or several, separated by commas
- The **start and end dates** you need
- Whether the client asked for a specific breakdown (by state, by site, by day, etc.)

### Where to run it

Slash commands work **anywhere in Slack** — a channel, a group DM, or a direct message with a colleague. Wherever you run it is where the report results will be posted. Pick the place you actually want the answer to land.

If you run it in a channel, make sure Analytics Bud has been added to that channel. If it can't post there, it will fall back to sending you a direct message.

---

## 3. Quick Start — Run Your First Report

1. Connect to the Cisco VPN.
2. Go to the Slack channel or DM where you want the results to appear.
3. Type `/form-report` and press Enter.
4. A window titled **Analytics Bud** opens.
5. Choose your **Report type** from the dropdown.
6. Enter the **Campaign ID(s)**, **Start date**, and **End date** (dates use the format `20260401` for April 1, 2026).
7. Leave **Metrics** and **Dimensions** blank for your first run — the defaults are the fastest option and usually answer the question.
8. Click **Run Report**.
9. Analytics Bud posts a message in that conversation saying it has started your report. A reply in that message's thread updates with live progress.
10. When it's done — usually within about 5 to 15 minutes — the finished report appears in the same thread, with an **Export CSV** button.

---

## 4. Using the Report Form

### How to open the form

| Command | What it does |
|---------|--------------|
| `/form-report` | Opens the report form. **This is the main one to use.** |
| `/analytics-bud form` | Opens the same form. |
| `/campaign-report` | Opens the same form, pre-set to Overall Campaign Performance. |

The window is titled **Analytics Bud**. The button at the bottom right is **Run Report**; **Cancel** closes the form without running anything.

### The fields

The form changes depending on which report you pick — not every report shows every field.

**Report type** (required, dropdown)  
The report you want to run. Changing this refreshes the rest of the form. **Important: changing the report type clears anything you already selected under Dimensions** — re-pick them after switching.

**The grey helper line under Report type**  
Shows which metrics and breakdowns the selected report supports. Read this before filling in the rest.

**Campaign ID(s)** (required for most reports)  
Numeric campaign ID, e.g. `231369`. For several campaigns: `231369,213651` (comma-separated, no spaces). On Pixel Fires this field is optional; on URL Pixels and DSP Pixel reports it does not appear.

**Start date (YYYYMMDD)** (required)  
Eight digits, no dashes. April 1, 2026 → `20260401`.

**End date (YYYYMMDD)** (required)  
Same format. On **Pixel Fires** only, the label reads "End date (YYYYMMDD, exclusive)" — confirm with your admin how to enter the last day you want included.

**Date range limit:** maximum **120 days**. The form rejects longer ranges. For speed and readability, use **14–30 days** for normal CS checks.

**Line item IDs** (optional)  
`12345,67890` — narrows the report when the client only cares about specific line items.

**Tactic IDs** (optional)  
`111,222` — same idea for tactics.

**Pixel IDs** (required on pixel reports)  
`20870477,20870479` — URL Pixels, Pixel Fires, and DSP Pixel Report only.

**Metrics** (optional, multi-select)  
See Section 6.

**Dimensions** (optional, multi-select)  
See Section 6.

### If something's wrong with your entry

When you click **Run Report** and something doesn't check out, Analytics Bud replies with a short warning that **only you can see**, explaining what to fix. Nothing was run. Open the form again and correct it.

---

## 5. Choosing the Right Report

Ten reports are available in Slack:

| The client is asking about… | Use this report |
|----------------------------|-----------------|
| Where delivery happened (DMA, state, city, zip) | **Geography Report** |
| Which sites, apps, and exchanges delivered | **Performance: Site/App/Exchange** |
| Overall performance with geo / time / site cuts | **Overall Campaign Performance** |
| Unique reach and average frequency | **Reach & Frequency (KS)** |
| Household impression-frequency buckets | **Frequency Buckets** |
| CTV / video by device, genre, app | **CTV Performance** |
| Unique impressed users vs clickers | **Impressed & Clickers by User** |
| Pixel fires by URL | **URL Pixels** |
| Detailed pixel fire log | **Pixel Fires** |
| Messaged vs unmessaged conversions | **DSP Pixel Report** |

### Report summaries

**Geography Report** — DMA, state, city, zip; CPA/ROAS.  
Metrics: impressions, clicks, spend, conversions, revenue, video starts, CTR, CPA, ROAS.  
Breakdowns: day, line item, tactic, creative, campaign, DMA, metro, city, state, zip, country.

**Performance: Site/App/Exchange** — Primary CS report for site/app questions (display, native, CTV, video).  
Metrics: impressions, clicks, spend, conversions, revenue, video starts, CTR, CPA, ROAS.  
Breakdowns: line item, tactic, creative, campaign, exchange, app, bundle, site. (Day not available.)

**Overall Campaign Performance** — Broad delivery with geo, time-of-day, day-of-week, site, app.  
Metrics: impressions, clicks, spend, conversions, reach, video starts, CTR, CPA, frequency.  
Breakdowns: day, line item, tactic, creative, campaign, state, DMA, metro, time of day, day of week, site, app.

**Reach & Frequency (KS)** — First-impression reach and impressions.  
Metrics: impressions, reach, frequency.  
Breakdowns: line item, tactic, campaign, campaign ID, line item ID, tactic ID.

**Frequency Buckets** — Household frequency distribution.  
Metrics: impressions, clicks, reach, household reach, CTR, frequency.  
Breakdowns: line item, campaign, frequency bucket.

**CTV Performance** — CTV/OLV by channel, device, genre, app.  
Metrics: impressions, video starts.  
Breakdowns: delivery channel, device type, device, genre, app, bundle.

**Impressed & Clickers by User**  
Metrics: **Unique Users (Sizmek Cookies)**.  
Breakdowns: user segment.

> **Important:** This report returns only the **total number** of unique users (Sizmek Cookies) — impressed vs clickers. It does **not** return individual Sizmek Cookies. If someone needs the actual cookie values, escalate to @Daniel Ohebshalom — do not expect that from Analytics Bud.

**URL Pixels** — Requires Pixel IDs. Messaged fires by URL / referrer.  
**Pixel Fires** — Requires Pixel IDs; campaign optional. Conversion fire log with geo and hierarchy.  
**DSP Pixel Report** — Requires Pixel IDs. Messaged vs unmessaged by conversion action.

### Check compatibility in Slack

```text
/analytics-bud compatibility
```

Full list of metrics and breakdowns per report. Reply is **visible only to you**.

```text
/analytics-bud list
```

Shorter list of available reports.

---

## 6. Choosing Metrics and Breakdowns

### Metrics

The **Metrics** field controls what appears in the Slack summary.

- **Select nothing** → Analytics Bud outputs **all applicable metrics** for that report.
- **Select specific metrics** → Analytics Bud outputs **only those**.

Selecting specific metrics keeps the output readable. When you combine several metrics with a breakdown (Date, Line item, etc.), every metric repeats on every row and the message gets bloated. Pick only what the client asked for.

Options marked **(n/a)** are not in that report — don't select them.

| Metric | Meaning |
|--------|---------|
| Impressions | Total impressions served |
| Clicks | Total clicks |
| Spend | Total media spend |
| Total conversions | Total conversions |
| Reach | Unique reach |
| Household reach | Distinct households |
| Revenue | Total revenue |
| Video starts / completes | Video events |
| CTR | Clicks ÷ impressions |
| CPA | Spend ÷ conversions |
| ROAS | Revenue ÷ spend |
| Frequency | Impressions ÷ reach |
| Messaged / Total fires, etc. | Pixel report counts |
| **Unique Users (Sizmek Cookies)** | Impressed & Clickers only — counts only |

CTR, CPA, ROAS, and Frequency require their underlying columns in the report.

### Dimensions

How results are **broken down** — by day, state, site, creative, etc. Options marked **(n/a)** aren't available for that report.

- **No dimensions** — fastest. Many reports still show automatic top-N sections (e.g. top states, top sites).
- **One or two dimensions** — sweet spot for specific client asks.
- **Three or more** — slower and very long in Slack. Prefer Export CSV for deep cuts.

Changing **Report type** clears Dimensions — re-pick after switching.

Slack shows **top rows** per section (often top 8). Use **Export CSV** for the full list.

### What makes a report slower

1. **Long date range** (biggest factor)
2. **Several dimensions at once**
3. **Many metrics combined with dimensions**
4. **Queue** — only one report runs at a time (Section 7)

### Recommended workflow

1. Report + campaign + **14–30 days**, no dimensions, no metrics selected.
2. Re-run with **one** dimension and only the metrics you need.
3. Widen dates or add a second dimension only if still needed.
4. **Export CSV** for full granularity.

---

## 7. Running a Report

1. Form closes after **Run Report**.
2. A message appears: *Analytics Bud started [Report Name]* (visible to everyone in that conversation).
3. A **thread reply** shows live progress.

Progress states you may see:

| Status | Meaning |
|--------|---------|
| Submitting to Hive | Handing off to the reporting system |
| Queued | Another report is running; yours waits (shows queue position) |
| Query submitted | Accepted, waiting to start |
| Still running | Executing — shows Query ID, progress bar, elapsed time |

**Query ID** — eight characters like `a3f7b2c1`. Save it for status, cancel, and export.

**Progress bar:** estimated from elapsed time, not exact work remaining. A slow bar does not mean failure.

**Do not re-submit** because it looks slow — duplicates queue behind the original.

**Cache:** Identical reruns within ~6 hours may return instantly (*"served from cache"*).

---

## 8. Checking Report Status

Use slash commands — not plain English.

```text
/analytics-bud status
```

Your active reports (Query ID, name, status, progress %, elapsed, campaign/dates).

```text
/analytics-bud status all
```

Everyone's active reports (queue visibility).

```text
/analytics-bud status a3f7b2c1
```

One report by Query ID.

Status replies post to the **Analytics Bud Messages tab** (Apps → Analytics Bud). From another channel you may see an ephemeral pointer to open Messages.

| Signal | Meaning |
|--------|---------|
| Still running / Queued in thread | Working |
| ✅ Query complete + results | Done |
| ❌ Query failed | See Section 13 |
| No active queries on status | Nothing running |

---

## 9. Cancelling a Report

```text
/analytics-bud cancel a3f7b2c1
```

Cancel one report (your Query ID).

```text
/analytics-bud cancel all
```

Cancel all **your** running reports. You cannot cancel someone else's.

Confirmation appears in Analytics Bud **Messages**.

---

## 10. Understanding Your Results

When complete:

1. ✅ **Query complete** — Query ID and total time.
2. **Results message** — summary, breakdowns, **Export CSV** button.

**Header** — report name, campaign, dates, filters, metrics/dimensions you chose.

**Overall result** / **Requested metrics** — campaign-level totals.

**Breakdown sections** — e.g. Top DMAs, Top sites. Each line shows metrics and often % of total.

**Footer** — runtime, row count, cache note if applicable.

**Tips:**

- Slack = summary + top rows, not a full grid → use CSV for everything.
- Daily reach summed across rows ≠ deduplicated unique reach → use Reach & Frequency for true reach.
- Impressed & Clickers = **counts** of Unique Users (Sizmek Cookies), not the cookies themselves.
- *No rows returned* → check campaign ID, dates, line item/tactic filters.

Re-show metrics from a finished report (within ~6 hours):

```text
/analytics-bud metrics a3f7b2c1 impressions,ctr,cpa
```

Reply visible only to you.

---

## 11. Sharing Results in Slack

### Forward the summary message

Use Slack **Forward message** / **Share message**.

> **Enable the message preview** — the option **"Show this message"** (or "Include message preview"). If you leave it off, the recipient only gets a **link they can't open** because they weren't in the original conversation. With preview on, the full report content travels with the share.

Run `/form-report` from the conversation where you want results to live when possible.

### Export CSV

Click **Export CSV** on the results message. Analytics Bud posts the file in the thread when ready. Click the filename to download.

Export from another conversation (within ~6 hours of completion):

```text
/analytics-bud export a3f7b2c1
```

CSV delivers where you run the command.

---

## 12. Common CS Use Cases

| Scenario | Form choices |
|----------|----------------|
| Monthly geo delivery | Geography Report · campaign · month dates · no dimensions |
| Site/app/exchange list | Performance: Site/App/Exchange · no dimensions · Export CSV |
| Site list for one line item | Same + **Line item IDs** |
| Reach & frequency | Reach & Frequency (KS) · metrics: impressions, reach, frequency |
| Frequency buckets | Frequency Buckets · no dimensions |
| Day-by-day pacing | Geography or Overall Campaign Performance · Dimension: **Day** · select only needed metrics |
| Creative comparison | Geography or OCP · Dimension: **Creative name** · metrics: impressions, clicks, CTR |
| CTV review | CTV Performance · optional Dimension: Genre |
| Unique users impressed vs clicked | Impressed & Clickers · counts only; escalate for actual Sizmek Cookies |
| Pixel / conversion questions | URL Pixels, Pixel Fires, or DSP Pixel Report + **Pixel IDs** |
| Client wants a spreadsheet | Simplest run (no dimensions) → **Export CSV** |

---

## 13. Troubleshooting & Escalation

| Problem | What to do |
|---------|------------|
| Typed a sentence; nothing happened | Use slash commands only (`/form-report`, etc.) |
| Hive MCP not reachable | Connect Cisco VPN; retry `/analytics-bud ping` |
| Report failed (❌) | Read error in thread; narrow dates; retry |
| Stuck progress bar | Normal if status = Running; don't re-submit |
| Validation warning after Run Report | Fix the field named in the ephemeral message |
| Date range > 120 days | Narrow dates or ask analyst outside Slack |
| Metric/dimension not available | Check compatibility line in form or `/analytics-bud compatibility` |
| Dimensions cleared | You changed Report type — re-select |
| Long queue | `/analytics-bud status all`; cancel your oversized run if needed |
| No rows returned | Verify campaign ID and delivery dates |
| Export/cache expired | Re-run report (~6 hour window) |
| Share recipient can't open link | Re-share with **Show this message** enabled |
| Status reply missing | Check Analytics Bud **Messages** tab |
| Bot can't post in channel | `/invite @Analytics Bud` |

### Who to contact

**@Daniel Ohebshalom** — Analytics Bud app issues:

- Wrong inputs, validation errors, failed or stuck reports
- Cancel/export/sharing problems
- Which report or breakdown to use
- Requests no report covers (including **actual Sizmek Cookie values**)

**Global IT Support (Jira ticket)** — access and infrastructure:

- Cisco VPN (connect, drop, credentials)
- Slack access, permissions, installing Analytics Bud

VPN or Slack → IT. What the app did or didn't do → Daniel.

---

## 14. FAQ

**How long does a report take?**  
Usually **5–15 minutes**. Long dates, many metrics, and multiple dimensions take longer.

**Can I ask in plain English?**  
No. Slash commands only, including in the Analytics Bud app window.

**One report at a time?**  
Yes — others queue automatically.

**Fewer metrics = faster?**  
Mainly cleaner output; shorten dates and dimensions to speed up.

**Cache?**  
Identical rerun within ~6 hours may return instantly.

**Cancel someone else's report?**  
No.

**Export window?**  
~6 hours after completion.

**Sizmek Cookies?**  
Impressed & Clickers gives **counts** only. Actual cookies → Daniel.

**Max date range?**  
120 days hard limit; 14–30 days recommended.

**Where do status/ping replies go?**  
Analytics Bud **Messages** tab.

---

## 15. Quick Reference

### Commands (slash only)

| Command | Purpose |
|---------|---------|
| `/form-report` | **Open report form** |
| `/analytics-bud form` | Same form |
| `/campaign-report` | Form → Overall Campaign Performance |
| `/analytics-bud ping` | Connection check (VPN first) |
| `/analytics-bud status` | Your active reports |
| `/analytics-bud status all` | All active reports |
| `/analytics-bud status <id>` | One report |
| `/analytics-bud cancel <id>` | Cancel one |
| `/analytics-bud cancel all` | Cancel yours |
| `/analytics-bud export <id>` | Download CSV |
| `/analytics-bud compatibility` | Metrics & breakdowns per report |
| `/analytics-bud list` | Report list |
| `/analytics-bud guidelines` | Best practices |
| `/analytics-bud metrics` | Metric definitions |

### Form fields

| Field | Notes |
|-------|-------|
| Report type | Required; changing clears Dimensions |
| Campaign ID(s) | Usually required |
| Start / End date | `YYYYMMDD`; max 120 days |
| Line item / Tactic IDs | Optional filters |
| Pixel IDs | Pixel reports only |
| Metrics | Empty = all applicable; select = only those |
| Dimensions | Empty = fastest; prefer 1–2 |

### Rules of thumb

- VPN → `/analytics-bud ping` → `/form-report`
- Slash commands only — not a chatbot
- 14–30 days · 5–15 min typical
- No dimensions first; add metrics when using breakdowns
- Forward with **Show this message**
- App issues → Daniel · VPN/Slack → Global IT (Jira)

---

## Open items (maintainers)

Items to confirm or align with the app over time:

1. In-app runtime estimates in the form/thread may read much longer than the 5–15 min CS guidance — consider aligning app copy with this guide.
2. Pixel Fires exclusive end date — document plain-English rule once confirmed.
3. Pixel Fires form label shows "Campaign ID (optional) (optional)" — cosmetic fix in app.
4. Reach & Frequency: "Line item" vs "Line item ID" — CS preference TBD.
5. Designated channel policy for CS runs — TBD.

When any item is resolved, update the relevant section above and note it in [Document history](#document-history).

