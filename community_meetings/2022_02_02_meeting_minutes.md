---
tags: SciPy
---

# 2022-02-02 Community Meeting

- Time: 12pm UTC (noon)
- Join via Zoom at https://zoom.us/j/93827717491?pwd=UGdkMzlnWEFjbDNQUmxpRkp6L0VLdz09 (or [dial-in](https://zoom.us/u/abpCzJ5DAn))

**Present:** Melissa Mendonça, Ralf Gommers, Pamphile Roy, Andrew Nelson, Akshay Ranade, Tyler Reddy, Carl Kleffner, Mukulika Pahari, Juan Luis, Namami Shanker, Evgeni Burovski, Ivan Yashchuk, Matti Picus (late), Mojca Miklavec

## Agenda

*Feel free to add items for discussion to this agenda!*

- Meeting frequency
    - *Consider meetings every two weeks with different time slots to include more contributors (all over the globe); e.g. a EU/Africa/Americas friendly time 1x/month, and a Pacific/Asia/EU friendly time 1x/month*
- Meetup frequency/organization/archiving/recording?
    - [github.com/scipy/archive](https://github.com/scipy/archive)
- Governance/maintainer/community update
- Summary of current grants (scope, timeline) & other potential/incoming funding. And how we apply for, decide on and manage that.
- Discuss website evolutions: scipy.org but also docs.scipy.org
    - Presentation of our websites' analytic dashboards
    - Melissa will look into the installation page (scipy.org/install) to review and possibly improve (quickstart as well)
    - API docs on mobile is not ideal. Could we raise this with the pydata-sphinx-theme folks?
- [SciPy2022](https://www.scipy2022.scipy.org) call for proposal ends soon
- Array API [issue](https://github.com/scipy/scipy/issues/15354) and [first PR](https://github.com/scipy/scipy/pull/15395)
    - Blog posts from Quansight Labs
        - https://labs.quansight.org/blog/2021/11/pydata-extensibility-vision/
        - https://labs.quansight.org/blog/2021/10/array-libraries-interoperability/
    - Some documentation from NumPy to understand the moving pieces: https://github.com/numpy/numpy/pull/20185
- Meson build system update
    - Need a decision on 32-bit windows (maybe discuss on https://discuss.scientific-python.org/)
- SciPy 1.8: issues? action points?
    - Tyler: 1.8.0 should be released this weekend I think 

- Social rules for feature contributions ("first send an email to the mailing list"), are they documented? How does the approval process work (one person saying "it's useful"? cool-off period of N days?)? Should they be included (linked) in the pull request template?
    - Having another discussion forum to reach maintainers and ping when you need help/reviews.
    - Look into codeowners file.

- I'm a new contributor and I have just raised a PR. How should I follow it up? Are there people in charge of specific submodules we could look to for help?

- Adding extra optimisers (based on C/Fortran libraries). 
    - Ideally, new optimizers should be Python, unless performance is not acceptable.

## Action items

- Melissa will look into the installation page (scipy.org/install) to review and possibly improve (quickstart as well)
- API docs on mobile is not ideal. Could we raise this with the pydata-sphinx-theme folks?

## For next meeting

- Blog posts? (journal like from users like https://scipython.com)
    - Proposal for a joint space between projects: blog.scientific-python.org
    - Like https://planet.scipy.org/?
- Backlog marathon?
