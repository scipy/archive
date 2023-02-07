---
tags: SciPy
---

# 2022-07-13 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa (@melissawm), Satish Mishra, Ralf Gommers (@rgommers), Will Tirone(@WillTirone), Evgeni Burovski (@ev-br), Anirudh Dagar

## Agenda

- [name=Pamphile] Sprinting 🏃 on Saturday at SciPy2022
    - Is this in-person only, or remote? --> announcement on mailing list would be nice
- [name=Pamphile] QMC+UNURAN talk at SciPy2022 on Thursday with Matt, Chris and Tirth
    - :tada:
- [name=rgommers] Doing a major bump in minimum GCC versions & allowing C++17: https://github.com/scipy/scipy/pull/16589
    - Would be nice to get more people to review
    - Ralf to also post on the mailing list before merging
    - Plan is to merge early in the 1.10.0 release cycle
- [name=Melissa] [Github labels](https://github.com/scipy/scipy/labels)
    - Can we clean up/improve the descriptions?
- [name=Melissa] [Unfixable issues on github](https://mail.python.org/archives/list/scipy-dev@python.org/thread/YGO5FQFUZCKRB7FGWKHXLXMIV6CACUAZ/) -- (Evgeni): repurpose the no-action label, maybe
- [name=rgommers] Moved datasets repos under the scipy org; moving forward `scipy.datasets`: https://github.com/scipy/scipy/pull/15607
    - Will make wheels smaller and enable adding new datasets
    - Make sure you participate in the discussion if this interests you
    - There will be documentation on caching the datasets locally
