# ElectoSQLytics: India Elections 2024 Analysis with SQL

**I turned 5 raw result files from the 2024 Lok Sabha election into clear answers: who won, where, and by how much,
using only SQL.**

`SQL Server` · `T-SQL` · `Joins` · `CASE WHEN` · `Aggregation` · `Data cleaning`

---

## The problem

The 2024 election results come as 5 separate tables: candidates, constituencies, parties, states and seat status.
On their own, they can't answer the questions people actually ask:

- Which **alliance** won, NDA or I.N.D.I.A? (The data has parties, not alliances.)
- Which **states** decided the result?
- Where were the **closest and biggest** wins?
- How much did **postal votes** matter?

## How I solved it

1. **Loaded** the 5 CSV files (8,902 candidate rows, 543 seats) into SQL Server.
2. **Linked** the tables with joins on constituency, party and state IDs.
3. **Created the missing alliance data:** added a `party_alliance` column and tagged every party as NDA, I.N.D.I.A
   or Other.
4. **Wrote 18 analysis queries** to answer each question at national, state and constituency level.
5. **Checked the data** and found an error in the source file (see Data notes).

## Results

| Alliance | Seats won | Share |
|---|---|---|
| **NDA** | **292** | 53.8% |
| **I.N.D.I.A** | **234** | 43.1% |
| Others | 17 | 3.1% |

**What the data shows:**

- **Coalition result:** NDA crossed the majority mark (272) by 20 seats, but BJP alone won 240, so partners
  TDP (16) and JD(U) (12) became essential.
- **5 big states decided it:** UP, Maharashtra, West Bengal, Bihar and Tamil Nadu hold 249 seats; I.N.D.I.A won 151.
- **Clean sweeps:** I.N.D.I.A won all 39 seats in Tamil Nadu; NDA won all 29 in Madhya Pradesh.
- **Uttar Pradesh:** Samajwadi Party (37 seats) beat BJP (33) as the state's largest party.
- **Margins:** from **48 votes** (Mumbai North West) to **11.75 lakh** (Indore).
- **Postal votes:** only 0.58% of votes, yet more than enough to flip a 48-vote seat.

## Data notes

- **Error found in source data:** Indore's row is labelled "Himachal Pradesh", but its State ID is Madhya Pradesh.
  My queries join on State ID, so the results use the correct state.
- Candidate rows include NOTA (542 rows), as the source lists it alongside candidates.

## What I'd improve next

- Move the alliance lists into a separate lookup table instead of repeating them in queries.
- Add a Power BI dashboard on top of these queries.

---

<details>
<summary>Files and how to run</summary>

| File | What it is |
|---|---|
| `1 SQLQuery_for_table.sql` | Checks the 5 tables loaded |
| `2 SQLQuery_for_analysis.sql` | All analysis queries |
| `*.csv` | The 5 source tables |
| `Project_Report.docx` | Full written report |

1. Create a database in SQL Server and import the 5 CSV files as tables.
2. Run `1 SQLQuery_for_table.sql`, then the sections of `2 SQLQuery_for_analysis.sql` one by one.

</details>
