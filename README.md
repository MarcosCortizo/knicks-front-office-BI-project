# Knicks Front Office

Power BI report on the New York Knicks 2025/26 season (the title year), with 2024/25 for comparison. I built it as a portfolio project to practise data modelling, DAX and report design with a dataset I collected myself.

The report has two parts:

- **Sports**: season overview, roster, health and availability, coaching staff and trades, league context.
- **Business**: MSG Sports finances, payroll vs the salary cap and aprons, value for money per player, arena attendance and partners.
There is also a hidden player profile page you reach by drill through from the roster.

## Model

Star schema with season, phase, team, player, date and game dimensions. Fact tables at season, game and series level, plus salaries, cap rules, injuries and financial statements.

Some things worth looking at:

- Calculation group (`Stat View`) to switch the roster between totals, per game and per 36.
- Field parameter for the league leaders chart.
- Small disconnected tables (`Team Stats`, `Cap Line`) to build comparison visuals with SWITCH.
- Power Query cleaning: splitting the awards column into rows, index column to keep the accounting order of the income statement.

## Data

- Basketball Reference: schedule, results, team and player stats, playoffs, rosters, coaches.
- ESPN public API: box scores.
- NBA official injury reports.
- Basketball Reference and Salary Swish: salaries.
- NBA Communications: salary cap, tax line and aprons.
- MSG Sports investor relations: financial statements and commercial agreements.

Data collected in October 2026. Currency USD.

## What I learned

- **Thinking like the front office.** Every page starts from a question a GM or a business director would ask, not from the data I had.
- **Data cleaning.** Splitting multi-value fields into rows, fixing types, and dealing with partial data like injury reports with no return date.
- **Data engineering.** A repeatable pipeline from raw CSV files with Power Query, one folder parameter and no manual steps.
- **Data modelling.** Star schema, one-to-many relationships, disconnected tables and a calculation group, keeping only the columns the report actually uses.
- **Charts.** Choosing the chart for the question: waterfall for where the money goes, sorted bars instead of a treemap, few colours with a fixed meaning.
- **Power BI.** DAX with context (CALCULATE, SWITCH, RANKX), field parameters, drill through, PBIP format and version control with Git.
- **Basics that matter.** Clear labels and units, saying what is an estimate, and removing anything that does not help the reader.

## Limitations

- Finance figures are for the whole MSG Sports group (Knicks and Rangers). The Knicks don't publish their own accounts.
- Committed salary adds every contract signed during the season, including players who were traded. It is not the cap payroll.
- Injury reports were extracted automatically and have no severity or return date.
- Sponsorship amounts are not disclosed.

## How to open

1. Clone the repo and open `knicks-front-office/Dashboard Knicks.pbip` in Power BI Desktop.
2. In Transform data > Manage parameters, point `CsvFolder` to the `knicks_csv` folder on your machine.
3. Refresh.

Marcos Cortizo Albiñana · [GitHub](https://github.com/MarcosCortizo)

Independent work. Not official NBA or New York Knicks data.
