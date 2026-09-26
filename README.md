# intern-hunt

Ranks live internship postings by how likely *you* are to actually get them, not by
how impressive the logo is.

Aggregator feeds are sorted by recency and dominated by companies that receive
thousands of applications per opening. For a sophomore with a short résumé, a list
sorted that way is mostly noise.

```
🎯 优先投这 6 个（命中率高）
 1 🟢 Visa — Software Engineer Intern, Sophomore Program   77  🎯 命中率高 🟢 限低年级
 2 🟡 Wex — AI & Data Platform Engineering Intern          66  🎯 命中率高
 3 🟡 Wells Fargo — SWE Intern, Early Careers              63  🎯 命中率高
 …

🎰 顺手投这 3 个（彩票，别指望）
 1 🟡 Waymo — Embedded Intern, Software Engineer           26  🎰 彩票厂 ⭐ 目标公司
 2 🟡 Google — Software Engineer Intern                    25  🎰 彩票厂 ⭐ 目标公司
```

## Scoring

Each of ~750 active postings is scored on 18 weighted signals: role track inferred
from the title, seniority and PhD markers, degree requirements, posting age,
location, remote flag, and visa-eligibility red flags.

**Ranking by hit rate, not brand.** Employers are classified by applicant-to-opening
ratio. Two calibration decisions that are not obvious:

- **Small ≠ reachable.** A 30-person AI startup with single-digit intern headcount is
  harder to get into than a large enterprise employer. Hot startups sit in the
  lottery tier alongside the megacaps.
- **Volume-hiring banks are not lotteries.** Goldman, JPMorgan, and Capital One each
  take hundreds of interns a year. They rank as reachable; proprietary trading firms
  with single-digit offers do not.

Reweighting this way surfaced a sophomore-specific program that brand-weighted
ranking had buried forty positions deep.

**Name matching is normalized.** Company names arrive inconsistently, so comparison
strips non-alphanumerics and gates short names to exact match — otherwise `AMD`
matches `Amdocs`, `SIG` matches `Signify Health`, and `JPMorgan` fails to match
`JP Morgan Chase`.

**Eligibility filters are advisory.** Postings that don't sponsor are flagged rather
than dropped — the filter is a label, not a gate, because the "no sponsorship" field
is frequently wrong.

## Usage

```
intern fetch                  refresh postings, diff against last run
intern digest                 build today's digest, push to Discord
intern list 10 [track]        browse the ranked pool
intern apply <n> [note]       record an application
intern skip <n>               suppress a posting permanently
intern lc 3 "LC 15/16/18"     log practice-problem count
intern status                 pipeline and weekly progress
```

## Setup

```bash
cp config.example.json config.json    # set profile, weights, target companies
./bin/intern fetch
```

Python 3, no dependencies. Postings come from the public
[SimplifyJobs](https://github.com/SimplifyJobs/Summer2027-Internships) feed and are
not redistributed here — `data/` is gitignored and rebuilt by `fetch`.

## Related

- [`study-log`](../study-log) — time tracking with enforced deliverables
- [`study-bot`](../study-bot) — Discord front end for both
