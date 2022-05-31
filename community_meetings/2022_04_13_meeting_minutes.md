---
tags: SciPy
---

# 2022-04-13 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonca, Inessa Pawson, Ralf Gommers, Gregory Lee, Pamphile Roy, Ross Barnowski, Tyler Reddy, Anirudh Dagar

## Agenda

- [name=Pamphile] If you have content ideas for the Scientific Python blog, please reach out to Pamphile or create an issue at https://github.com/scientific-python/blog.scientific-python.org
- [name=Melissa] [Developer CLI for SciPy](https://github.com/scipy/scipy/pull/15959)
    - If you have feedback or suggestions, please leave a comment in the PR
- [name=Melissa] [Revamp contributor setup guides](https://github.com/scipy/scipy/pull/15947)
    - Looks good! Close to being merged.
    - Removing the `building/` directory completely seems right, it was mostly outdated and there's no real reason to have both `building/` and `contributing/` with a lot of overlap.
- [name=Melissa] Sprints
    - DataUmbrella 
        - June 25th
    - PyCon US’22
        - Select a few issues and add a “sprint” label to them
        - Mentored sprints April 30, regular developer sprints May 2-3
            - Mentored sprints are more structured, but should be focused on newcomers. Do we have mentors available? What would be best for the issues we have available?
            - Pamphile, Anirudh, & Tyler tentatively volunteer to help
        - Send an email to the mailing list to ask if more people want to participate

- [name=Melissa] SciPy development workflow video (https://www.youtube.com/watch?v=HgU01gJbzMY)
    - From 2018, 350 views.
    - Data Umbrella sprint: Reshama (organizer) asked Melissa to record a similar video, so she will likely do that.
    - A new recording needs to be made more discoverable - the low view count is very likely simply a proxy for discoverability.
    - Put the script for the recording in `scipy/archive`.

- [name=Ralf] thoughts on [Ralf's email about undermaintained submodules & SciPy project priorities](https://mail.python.org/archives/list/scipy-dev@python.org/thread/V5ADHAFNZIRTQXZL5DHGXA7NDT5DELRS/)?
    - For some submodules such as scipy.signal it might be best to create a new submodule entirely.
    - Should we have a more concrete plan for SciPy (SciPy 2.0, for example) or go with priorities for each submodule independently?
    - It is hard for the current maintainers (a few who are not very involved in the day-to-day development) to prioritize and mentor new contributors. Even reviewing PRs has proven difficult.
    - We could have people focusing on algorithms and the theoretical parts, and others reviewing code quality.

- [name=Pamphile] our talk about sampling (UNURAN + QMC) is accepted for SciPy2022 :tada: 

- [name=rossbar] General poll: are there use-cases that you know of for older (<4) sphinx?
  * I know this occurs in scipy CI
  * Jinja 3.1 broke older versions of Sphinx (<4.1.2) and numpydoc will also break for those older Sphinx versions.

- [name=Pamphile] Version switcher from the pydata-sphinx-theme is merged
    - If we want to retire the legacy page with all previous versions, how do we manage the .zip and .pdf files currently linked there?
    - One idea is to customize the dropdown items for the menu and add the links there (may require a PR to pydata-sphinx-theme)

- [name=Tyler] We need to think of a solution for .htaccess and releases so the docs links don't break again in the future.
    - Tyler has documentation on that
