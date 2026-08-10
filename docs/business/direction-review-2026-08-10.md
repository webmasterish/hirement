# Direction review, 2026-08-10


Where hirement.com actually stands and what the options are. Written after
pulling Matomo, Google Search Console and Ahrefs data on the same day. No
decision was made. The owner is sleeping on it.

All figures are as of 2026-08-10. Raw exports are in `__/data/`, gitignored.


********************************************************************************

## Summary


The site grew 10x in two years with no maintenance, but the growth is not worth
what it looks like. Around 95% of search traffic comes from people searching for
another company's brand name and landing on hirement's page about that company.
There is almost no traffic of hirement's own, and Google is steadily deindexing
the site.

Revenue is $0 and always has been. The traffic is too small and too low-intent
to sell anything to. The realistic assets are the domain, the 442 referring
domains, and the catalogue of 371 job boards, not the visitors.

The lever on any exit is having any revenue at all, not more traffic.


********************************************************************************

## The data


--------------------------------------------------------------------------------

### Traffic (Matomo, idSite 3)

| Period | Visits |
| --- | --- |
| 2024 | 1,727 |
| 2025 | 5,669 |
| 2026, to Aug 10 | 8,750 |

Around 1,600 visits/month and climbing. Last 12 months: 12,134 visits, 28,814
actions, 2.4 actions/visit, 53% bounce.

- Sources: search 63%, direct 35%, AI assistants 145 visits, websites 43,
  social 9.
- Countries: US 2,653, India 2,001, Pakistan 683, Nigeria 593, Canada 343,
  Kenya 250.
- Devices: 70% desktop.

Unverified doubts: direct entry is 4,298 visits at 79% bounce against 40% for
search, which looks like bots. China contributes 333 visits at 99% bounce.


--------------------------------------------------------------------------------

### Search queries (GSC, last 16 months)

1,000 queries, 6,601 clicks, 658,045 impressions, CTR 1.00%.

| Bucket | Queries | Clicks | Share |
| --- | --- | --- | --- |
| Destination brand names | 210 | 5,464 | 82.8% |
| "Generic" | 786 | 1,052 | 15.9% |
| Hirement's own brand | 4 | 85 | 1.3% |

The generic bucket is mostly brands the classifier missed: datayoshi,
welovenocode, justremote, authentic jobs, joblist ai, remotehunt, useweb3,
ninjajobs, hasjob, career vault, workello, working nomads, gitmatcher.

Filtering for queries that contain a real category descriptor ("best", "list
of", "job boards", "remote jobs", "how to") gives 247 queries producing **162
clicks, 2.5% of all search traffic**.

Ahrefs reaches the same conclusion independently. Its brand attribution of
hirement's organic traffic: other brands 118, non-branded 43, own brand 5. It
names the entities it believes the traffic belongs to: SkipTheDrive, Support
Driven, TrueUp, Data Elixir, TrueIO.

High visibility, near-zero conversion, because the searcher wants the
destination and hirement sits at position 7:

| Query | Impressions | Clicks | CTR |
| --- | --- | --- | --- |
| remote4me | 92,881 | 416 | 0.45% |
| rxresu.me | 66,965 | 227 | 0.34% |
| jobspresso | 37,071 | 49 | 0.13% |
| skipthedrive | 20,341 | 12 | 0.06% |

A handful are outranked outright: rubynow at position 1.33 with 31% CTR,
wphired at 2.14 with 33%, js remotely at 3.59 with 16%. That normally means the
destination is weak or gone. jsremotely is known to redirect elsewhere now. The
rest have not been checked and there is no plan to check them.


--------------------------------------------------------------------------------

### Indexing (GSC)

- Indexed 415, not indexed 788.
- Crawled, currently not indexed: 638 pages.
- Duplicate without user-selected canonical: 125 pages.
- Discovered, currently not indexed: 23 pages.

Indexed count was ~500 in mid-May, fell to 352 in early July, recovered to 415.
Two thirds of the site is crawled and rejected. That is Google's verdict on
listing pages that restate the destination's own description.


--------------------------------------------------------------------------------

### Off-site (Ahrefs, free Webmaster Tools)

- Referring domains: 442, 4 new that week. The healthiest number in the set.
- Organic pages producing traffic: 38, out of 371+ listings.
- Estimated organic traffic value: $30/month.
- AI Overview presence: 1. Effectively no AI search visibility.


--------------------------------------------------------------------------------

### Referral flow (Matomo outlinks)

8,195 outbound clicks over 12 months across 371 destinations, all tagged
`?ref=hirement`. Top: wphired 901, kickstartremote 686, jsremotely 529,
wesellremotely 178, meterwork 177, flexhired 159, rxresu.me 139.

Read this in light of the query data. These are not discoveries. They are mostly
people who already knew the destination's name, searched it, and were routed
through hirement. From the destination's side that reads as interception, not
referral, which badly weakens any pitch to sell them placement.


--------------------------------------------------------------------------------

### Revenue

$0, always. TinyAdz, added 2025-04-17, has produced $36.81 in about 16 months
against a $100 payout threshold. 2,387 ad views, 158 verified clicks. Display
advertising on this traffic volume is not a path to anything.


********************************************************************************

## Valuation


Small sites price at 30-40x monthly net profit. At $0 profit that returns
nothing, so a zero-revenue site is priced on traffic and assets at a heavy
discount, commonly $0.50 to $2 per monthly visitor.

| Scenario | Range |
| --- | --- |
| As-is, $0 revenue, marketplace listing | $1,000 - $3,000 |
| Domain alone, brandable marketplace | $500 - $2,500 |
| After 3-6 months at $150-300/month net | $4,500 - $12,000 |

These are rules-of-thumb estimates, not comparable-sale research.

The site was listed on `acquire.website` on 2024-06-13 at $1,500, a price
suggested by that marketplace's owner, and drew no serious offers. That range
still roughly holds despite 10x the traffic, because revenue is still $0 and
there is now a visible deindexing problem any buyer can see in Ahrefs or GSC.

Conclusion: three months of $200/month is worth more to the exit price than
another year of traffic growth.


********************************************************************************

## Where it could be sold


Most marketplaces are closed. Empire Flippers wants $10k minimum and 12 months
of revenue history; Investors Club and Motion Invest also want revenue.

Open routes:

- Flippa. Built for sub-$10k sites. Listing fee plus roughly 10% success fee,
  and a lot of tire-kickers.
- Tiny Acquisitions, Side Projectors. Sub-$5k projects, smaller audience, less
  noise, faster.
- Acquire.com. Free to list, skews SaaS.
- Domain-only exit via Dan, Afternic, Sedo, or a brandable marketplace like
  Atom. Slower, but `hirement.com` is a clean one-word pronounceable .com in a
  high-commercial-value niche, which is the profile those price well.

The highest-value route is direct outreach, not a marketplace. hirement ranks on
page one for the brand names of 210 job boards. To a competitor of any of those
boards, that is a permanent position on a rival's search results. That buyer
type is the only one for whom the branded-traffic problem is a feature rather
than a defect, and they are not paying $1,500. Five emails cost an afternoon.


********************************************************************************

## Monetisation options besides ads


The binding constraint: 1,600 visits/month of job seekers weighted to India,
Pakistan, Nigeria and Kenya, arriving on navigational searches. Low commercial
intent, low willingness to pay. Nothing sold to these visitors clears more than
a few hundred dollars a month. The better products do not sell to them at all.

Ranked by expected value against effort:

1. **The job board dataset.** 371 boards already catalogued, with a year of
   click data on each. Cleaned into a spreadsheet or Notion database with niche,
   submission URL, cost to post, audience size, contact and status, this sells
   at $29-49 to recruiters, HR staff, outreach marketers and people launching
   job boards. Sold off-site through Gumroad, so the weak site traffic is
   irrelevant. The one asset nobody else has, and the build is largely a
   database export.

2. **Resume and tooling affiliate links.** The query data proves the demand:
   rxresu.me variants pulled 293 clicks and people arrive looking for a free
   resume builder. Resume builders, ATS checkers and course platforms all run
   affiliate programs, and course affiliates convert on an India/Nigeria-heavy
   audience. 8,195 outbound clicks a year currently leave for free. Realistically
   a few hundred dollars a year, but close to zero effort and it puts revenue on
   the books, which is what the valuation needs.

3. **A paid resume pack** at $9-19. Plausible on the same demand signal, but at
   sub-1% conversion expect $50-150/month at best. Test with a landing page
   before building.

4. **Selling placement to the destinations.** Much weaker than the raw outlink
   count suggests, for the interception reason above. Worth a cheap test on the
   top five, expecting a low hit rate.

Rejected:

- Post-your-job distribution as a service, the genuinely profitable version of
  this niche at $200-500 per posting, needs employer traffic. This site has job
  seeker traffic. Wrong side of the marketplace.
- Newsletter. Mailster is installed and the list is empty. At this traffic that
  is a two-year project and job seeker lists monetise poorly per subscriber.
- Job board status tracker / "graveyard" record. Considered and dismissed by the
  owner: not something anyone would pay for.


********************************************************************************

## Recommended sequence


Keeps sell, park and rebuild all open, and raises the exit number at each step.

1. Send five emails to strategic buyers, meaning competitors of the boards
   hirement outranks. Cheapest, highest upside, and the replies price the asset
   better than any marketplace listing would.
2. In parallel, put affiliate links on the resume and tooling listings. Weeks,
   not months. Starts the revenue clock.
3. Build the job board dataset as a Gumroad product. Boring, off-site,
   monetises the catalogue instead of the traffic.
4. Reassess in three months. With $200/month on the books, list at a profit
   multiple. Without it, list as-is or take the domain exit.


********************************************************************************

## Open questions


- No decision yet. The owner is sleeping on it.
- Is the direct traffic real or bots? 4,298 visits at 79% bounce is unexplained.
- How many of the 371 destinations are still alive? Deliberately not checked.
  jsremotely is known to redirect elsewhere.
- What is the Adzuna API key in `wp/.config/api_keys.php` for? Nobody remembers.
  A grep of the theme would settle it.
- Whether to connect GSC properly. Needs a Google Cloud project, the Search
  Console API enabled, a service account added as a Restricted user on the
  property, and either a community MCP server or a short script in `ops/`
  writing to `__/data/gsc/<date>/`. Gets past the 1,000-row UI export cap. Not
  worth building unless the decision is to keep and grow.


********************************************************************************

## Sources


- Matomo, DotAim instance, `idSite=3`, via the MCP connector.
- GSC Performance on Search, last 16 months, and Coverage, exported 2026-08-10
  to `__/data/gsc/2026-08-10/`.
- Ahrefs free Webmaster Tools, three performance exports plus overview
  screenshots, `__/data/ahrefs/2026-08-10/`.
- TinyAdz dashboard screenshot, `__/screenshots/`.

Marketplace multiples and per-visitor ranges are general market rules of thumb,
not researched comparable sales. Tighten them before acting on a price.
