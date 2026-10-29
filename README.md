# SaloneMove

**A Commuter Fare Check and Reporting System for Freetown**

PROG101 Principles of Programming Logic and Design: Individual Assignment
*Designing Logical Solutions for Sierra Leone Community Challenges* (community problem: Transportation)

| | |
|---|---|
| **Student name** | Mohamed Bashir Jalloh |
| **Student ID** | [StudentID] |
| **Programme / Intake** | [Programme / Intake] |
| **University** | Limkokwing University of Creative Technology, Sierra Leone |
| **Module** | PROG101 Principles of Programming Logic and Design |
| **Examiner** | Elijah Fullah |
| **Semester** | 01 (September 2026 to January 2027) |

> **Status:** revised submission, following examiner review. See [Revisions after review](#revisions-after-review).

---

## The problem

Most people in Freetown travel by poda-poda, shared taxi, okada or keke. These four modes carry about 92% of passenger demand. Fares are set by government and change whenever fuel prices change. For example, the fare list that took effect on 30 June 2026 cut the Lumley to Regent Road poda-poda fare from NLe 7.00 to NLe 6.10.

New fare lists are shared through press releases, radio and social media. Only about one person in five uses the internet, so many commuters never see the new fares. That leaves passengers with three problems:

- They cannot easily check the official fare for a trip.
- They cannot tell whether they have been overcharged.
- They have no simple way to report a driver.

Regulators also have no organised record of where these problems happen.

## The solution

SaloneMove is reached through a **USSD short code with SMS replies**, so it works on any mobile phone, without data or an app. It offers four services:

| Service | What it does |
|---|---|
| **Phone validation and verification** | *Validation* checks that the caller typed a correctly formed Sierra Leone mobile number: 9 digits starting with a valid mobile prefix, with 3 attempts. *Verification* then texts a one-time 6-digit code to that number. The code must be typed back within 5 minutes, with 3 tries, which proves the caller holds the phone. |
| **Check a Fare** | Gives the official fare for a route and vehicle. It then says whether the amount paid was **underpaid**, **correct**, **overcharged** or a **serious overcharge**. |
| **Report a Problem** | Records overcharging, short-routing, reckless driving, harassment or overloading against a route, and sends an SMS reference number such as `SLM-2026-000011`. An overcharging report is accepted only if the fare check found an overcharge. |
| **Officer Portal** | Protected by a PIN that locks after 3 wrong tries. Lists hotspot routes with 3 or more open complaints, and applies a government fare change to every fare in one step. |

Every number, menu choice and place name is checked before it is used. A clear message says what is wrong and asks again, so a mistyped entry never stops the system or saves bad data.

![Structure chart](flowcharts/structure_chart.png)

## Repository contents

| Folder / file | Contents |
|---|---|
| `README.md` | This file |
| `LICENSE` | MIT licence for the pseudocode and any code (see [Licence](#licence)) |
| `report/` | The full assignment report: `SaloneMove_Report.docx` and `SaloneMove_Report.pdf` |
| `algorithm/` | `SaloneMove_algorithm.md`: the step-by-step algorithm in plain English |
| `pseudocode/` | `SaloneMove_pseudocode.txt`: the complete pseudocode |
| `flowcharts/` | The four flowcharts and the structure chart, as editable diagrams.net files (`.drawio`) and images (`.png`) |
| `screenshots/` | Repository and commit-history screenshots used as evidence in the report |

```
PROG101_Assignment1_[StudentName]_[StudentID]/
├── README.md
├── LICENSE
├── report/
│   ├── SaloneMove_Report.docx
│   └── SaloneMove_Report.pdf
├── algorithm/
│   └── SaloneMove_algorithm.md
├── pseudocode/
│   └── SaloneMove_pseudocode.txt
├── flowcharts/
│   ├── flowchart1_main.drawio, flowchart1_main_part1.png, flowchart1_main_part2.png
│   ├── flowchart2_check_fare.drawio, flowchart2_check_fare_part1.png, flowchart2_check_fare_part2.png
│   ├── flowchart3_report_problem.drawio, flowchart3_report_problem.png
│   ├── flowchart4_officer_portal.drawio, flowchart4_officer_portal_part1.png, flowchart4_officer_portal_part2.png
│   └── structure_chart.drawio, structure_chart.png
└── screenshots/
    ├── repository_home.png
    └── commit_history.png
```

## Flowcharts

There are four flowcharts, one for each part of the system. Each shows a module together with the functions it calls, drawn as separate START … RETURN flows. Flowcharts 1, 2 and 4 continue on a second page.

| Flowchart | Shows | Files |
|---|---|---|
| 1. Main program | `Main()`, `IsValidPhone()`, `VerifyPhone()`, `ReadChoice()` | [part 1](flowcharts/flowchart1_main_part1.png), [part 2](flowcharts/flowchart1_main_part2.png) |
| 2. Check a Fare | `CheckFare()`, `FindFare()`, `ClassifyFare()`, `ReadPlace()`, `ReadNumber()` | [part 1](flowcharts/flowchart2_check_fare_part1.png), [part 2](flowcharts/flowchart2_check_fare_part2.png) |
| 3. Report a Problem | `ReportProblem()`, `IsValidPlate()` | [image](flowcharts/flowchart3_report_problem.png) |
| 4. Officer Portal | `OfficerPortal()`, `GenerateHotspotReport()`, `ApplyFareAdjustment()` | [part 1](flowcharts/flowchart4_officer_portal_part1.png), [part 2](flowcharts/flowchart4_officer_portal_part2.png) |

Each flowchart uses exactly the same statements, names and messages as the pseudocode, so the two can be read side by side.

### Opening the flowcharts in diagrams.net

1. Go to [app.diagrams.net](https://app.diagrams.net) (free, no account needed).
2. Choose **Open Existing Diagram**, or **File → Open from → Device**, and select a `.drawio` file from the `flowcharts/` folder.
3. For a flowchart with two parts, switch between **Part 1** and **Part 2** using the page tabs at the bottom of the window.

You can also open the files in the free desktop app (diagrams.net / draw.io), or in VS Code with the *Draw.io Integration* extension.

## Programming logic covered

| Concept | Where it is used |
|---|---|
| **Modular design** | 6 modules (`Main`, `CheckFare`, `ReportProblem`, `OfficerPortal`, `GenerateHotspotReport`, `ApplyFareAdjustment`) and 8 functions (`IsValidPhone`, `VerifyPhone`, `ReadChoice`, `FindFare`, `ClassifyFare`, `ReadPlace`, `ReadNumber`, `IsValidPlate`) |
| **Data types and structures** | INTEGER, REAL, STRING, BOOLEAN, DATETIME; constants; records (`FareRecord`, `Complaint`); arrays |
| **Decisions** | IF, IF … ELSE, nested IF, IF … ELSE IF … ELSE (four fare statuses), CASE (main menu) |
| **Repetition** | WHILE with a counter and a flag (3 attempts); flag-controlled menu loops; WHILE search with early exit; WHILE with a priming read (input checks); FOR; nested FOR (hotspot counting) |
| **Boolean logic** | AND, OR, NOT; e.g. `sameVehicle AND sameRoute`, `entry = code AND elapsed ≤ CODE_EXPIRY_SECONDS` |
| **Searching** | Linear search of the fare table, matching routes in either direction and ignoring capital letters |
| **Input validation and error handling** | Every entry is read as text and checked before conversion; range checks; attempt limits on phone, code and PIN; division-by-zero guard; SMS-failure handling |

### Fare classification

`difference = amount paid − official fare` and `percent = difference ÷ official fare × 100`. The tolerance of NLe 0.50 allows for lack of small change.

| Condition | Status |
|---|---|
| difference < −0.50 | `UNDERPAID` |
| −0.50 ≤ difference ≤ 0.50 | `CORRECT` |
| difference > 0.50 and percent < 50 | `OVERCHARGED` |
| difference > 0.50 and percent ≥ 50 | `SERIOUS OVERCHARGE` |

### Testing

The design was desk-checked with:

- 12 test scenarios, each traced through both the pseudocode and the flowcharts
- 4 error-handling tests
- boundary tests for every fare status

Together they pass through every box and every Yes/No and CASE path at least once. The test data uses:

- the official poda-poda fares from 30 June 2026
- invented complaints
- officer PIN `2468` (stored only as a hash)
- a fixed one-time code of `482913`

Full expected outputs are in Section 6 of the report.

## Revisions after review

The examiner asked for three changes. The original design, its six modules and its four flowcharts were kept, and only these parts changed:

1. **Phone verification.** The old format check is now correctly called *phone number validation*. It is also stricter: the number must start with a Sierra Leone mobile prefix. A real *verification* step was added, which sends a one-time SMS code with 3 tries and a 5-minute expiry.
2. **Fare classification.** `ClassifyFare()` now separates **underpaid**, **correct**, **overcharged** and **serious overcharge**. Before, paying less than the fare was wrongly called "FAIR".
3. **Input validation and error handling.**
   - `ReadChoice()`, `ReadNumber()` and `ReadPlace()` check every entry before it is used.
   - The officer PIN locks after 3 wrong tries.
   - A damaged fare record cannot cause division by zero.
   - SMS failures are reported to the user.

## Sustainable Development Goals

| SDG and target | How SaloneMove contributes |
|---|---|
| **SDG 11.2**: safe, affordable, accessible transport | Makes official fares known on any phone and protects passengers from overcharging |
| **SDG 3.6**: fewer road traffic deaths and injuries | Reckless driving and overloading reports identify dangerous routes and vehicles |
| **SDG 16.6**: accountable, transparent institutions | Every complaint gets a reference number and is counted |

## Open source and Digital Public Good

SaloneMove handles public fare data and public complaints, so the logic that decides what counts as "overcharged" should be open for anyone to inspect. Being open source means:

- no licence fees for government
- no lock-in to a single vendor
- the design can be adapted for Bo, Kenema, Makeni or inter-district routes
- local students and developers can maintain and extend it

The project is designed to meet the nine indicators of the [Digital Public Goods Standard](https://www.digitalpublicgoods.net/standard):

- relevance to the SDGs above
- open licences (below)
- clear ownership (proposed: Sierra Leone Public Transport Authority)
- open standards (USSD and SMS)
- published documentation
- open export of non-personal data (fare tables and anonymised complaint counts)
- privacy: only the verified phone number is stored, and one-time codes are never stored
- standard practices: modular design, version control and validation of every entry
- do no harm: hashed PIN with lock-out, reports only from verified numbers

## Licence

- **Pseudocode and any source code** are released under the [MIT Licence](LICENSE).
- **Documentation** (the report, algorithm, flowcharts and images) is released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You may share and adapt it for any purpose, as long as you give appropriate credit.

## Key sources

- World Bank (2024) *From teetering to thriving: Transforming public transportation in Sierra Leone*. https://blogs.worldbank.org/en/transport/from-teetering-to-thriving--transforming-public-transportation-i
- Sierraloaded (2026) *Government announces new public transport fare following fuel price reductions*, 1 July. https://sierraloaded.sl/news/government-public-transport-fare-fuel-eductions/
- DataReportal (2026) *Digital 2026: Sierra Leone*. https://datareportal.com/reports/digital-2026-sierra-leone
- United Nations (2015) *Transforming our World: the 2030 Agenda for Sustainable Development*. https://sdgs.un.org/2030agenda

The full reference list is in Section 8 of the report.
