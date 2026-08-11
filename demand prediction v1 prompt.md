ok so i think we can surface on a mobile page, the counts, so they can look at it, and use it to prefill their own clipboard

then they can get a recommendation by hitting a button with whatever data they've entered (this part might require more thinking)                                                
Good insight, and it collapses a problem: staff already write times/unsold-counts on the paper clipboard by hand throughout the day — asking them to also type that into a phone
  in real time is double work and the classic way these tools get abandoned. So the natural design:

  - Morning: mobile page shows recommended bake counts → they use it to fill in the paper clipboard like today.
  - End of day: someone snaps one photo of the completed sheet (exactly like the ones you sent me) and uploads it on the same mobile page.
  - Button: "Get Recommendation" triggers OCR extraction on that photo → shows a quick confirm screen (since handwriting has real ambiguity — crossed-out numbers, "+10?",
  overlapping digits) → on confirm, it commits to the DB and computes next week's numbers.

  This means the vision-extraction pipeline isn't just a one-time historical-backfill script — it's core, always-on infrastructure, reused for both the weekly loop and digitizing
  the 3-year binder backlog later. Worth building well from the start rather than as a throwaway migration script.

  That also settles the stack question in my head: this needs a real interactive app (photo upload, OCR call, confirm step, DB, recommendation view) — pointing at Next.js + 
  Postgres (Railway), which matches what's already wired up in your environment. Does that match what you had in mind, or were you picturing something lighter for the entry side
  (e.g. skip the confirm step, or let them type corrections instead of re-photographing)?

---

i talked to the midwife and the baker and they could use some help with predicting demand to maximize sales, and to minimize waste

they manually record all of their data, going back three years

i've managed to get 10 weeks of data (via pdf), this is in /public/midwife-10weeks.pdf

i want to create a tool that helps them
1. be better about predicting demand for the week for their products
2. reducing the amount of waste and products that don't get sold

i see it like this:
- [ ] pdf/csv/api pipeline ingestion to psql or csv
- [ ] historical data cleaning to standardized formats, and fixing missing values
- [ ] data rules, how to interpret the data
- [ ] think about metrics, analysis, rate of consumption, trends, rolling average, MoM, YoY
- [ ] final recommendation for the upcoming week as a pdf printout, or csv
- [ ] after the week is over, data ingestion pipeline for the latest week and a comparison of the recommendation before the week started to actual after week results
- [ ] repeat, recommendation for the upcoming week

i'd also like to generalize this process into skills that we can reuse for every bakery/cafe/restaurant, so reusable skills should be another outcome we can think about surrounding demand prediction