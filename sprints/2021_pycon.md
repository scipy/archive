# SciPy PyCon sprint

## Organization


[//]: # (Note that intro to the sprint will be done by the PyCon organizers and is common between SciPy and other projects)



## Post-sprint


For continued support and following up on your pull requests:
* Reach out to SciPy on their [mailing-list](https://scipy.org/scipylib/mailing-lists.html) or [GitHub](https://github.com/scipy/scipy).  
* Open an issue or comment on an [issue](https://github.com/scipy/scipy/issues).



## The Team

### SciPy Mentors (all Core Contributors)
SciPy is a library that is used around the world. Open source sprints are typically limited to where contributors live or where major conferences are held.  We are fortunate to have support from several SciPy contributors: 

* Ralf Gommers (https://github.com/rgommers) - EU time slot, Sat
* Pamphile Roy (https://github.com/tupui) - EU time slot, Sat
* Matt Haberland (https://github.com/mdhaber) - US time slot, Sun
* Warren Weckesser (https://github.com/WarrenWeckesser) - US time slot, Sun


### Mentored Sprints
[Mentored Sprints](https://mentored-sprints.netlify.app/) was created in an open effort to tackle some diversity and inclusion issues in the open-source community. They have been very supportive of us and this sprint, hosting us on their discord server. 
* Tania Allard (https://www.mentored-sprints.dev/team/)


## Purpose of Sprint
- Help newcomers contribute to the SciPy library
- Involve more women, gender minorities and other people from underrepresented group in SciPy and the Python open source community
- Build momentum for continued contribution


## Goals for the Day
- The plan is to work in pairs/small groups. 
- The goal is that each participant will be able to resolve one issue and submit a pull request (PR).


---
## Preparation

### 1.  GitHub Account
- Open an account on [GitHub](https://github.com/)
- [Git should be installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- Some familiarity with Git / GitHub 
- Prior to event, review some [Git resources](https://github.com/reshamas/git-intro-workshop/blob/master/extra_resources/resource_git_tutorials.md) 
- We will go over pull requests at beginning of event

### 2.  Join [Discord](https://discord.com/)
Discord is a voice, text and video communication platform that allows us to set both text and voice channels.
We are using the [Mentored Sprints](https://www.mentored-sprints.dev/) Server on Discord for the sprint to help mentors support participants and enable us to pair program. 
Participants will be invited to join and connect via the Discord Server during the pre-sprint setup.

A beginners guide to discord can be found [here](https://support.discord.com/hc/en-us/articles/360045138571-Beginner-s-Guide-to-Discord).


### 3.  Read through the [SciPy Contributing documentation](https://scipy.github.io/devdocs/dev/contributor/contributor_toc.html)

* The following documentation will help you setup and build a local development environment:
    - [Fork and configuration of SciPy repository](https://scipy.github.io/devdocs/dev/gitwash/development_setup.html)
    - [Build SciPy](https://scipy.github.io/devdocs/dev/contributor/contributor_toc.html#development-environment)
    - There is an alternative option to use the SciPy Gitpod setup _(this works without having to install anything, you can get coding straight away!)_.  More information can be found [in the SciPy Gitpod docs](https://scipy.github.io/devdocs/dev/contributor/quickstart_gitpod.html#quickstart-gitpod). Use `pytest scipy/io` or (e.g., within IPython) `>>> from scipy import io; io.test()` to run tests here (works for any submodule, or scipy as a whole).


* General guidelines for contributing:
    - Read through the recommended [development workflow](https://scipy.github.io/devdocs/dev/contributor/development_workflow.html#development-workflow)
    - Read through how-to [guide to contributing to SciPy documentation](https://numpy.org/devdocs/dev/howto-docs.html) (same as NumPy)

### 4. Choosing an issue to work on
* [Use the list of issues labelled with `sprint-pycon`](https://github.com/scipy/scipy/issues?q=is%3Aissue+is%3Aopen+label%3Asprint-pycon) to find a good starter issue.
* Please comment on the issue that you are working on it. This avoids multiple people taking on the same issue.
* Other approachable issues are labelled with [`good first issue`](https://github.com/scipy/scipy/labels/good%20first%20issue)
* There are over 2000 issues :sweat:. If you search for an issue not labelled `pycon-sprint`, it is recommended to pick issues that is relatively new and doesn't have too many comments on it.
	- old issues are often difficult to solve or unresolvable which is why they still remain
* The selections in `sprint-pycon` are focused on beginner-to-intermediate-friendly issues that are actionable and should be doable today. If you want to take on something a little more challenging, there are a lot of issues on the main repo to choose from. Try to choose issues that (from the title or labels) seem to be bugs, and don't have more than 5 comments - those are most likely to be actionable.


---

## Get Sprinting! (aka fixing Issues and submitting a PR!)
Here are a few more useful links and guides to follow:
### Documentation Issues
If you are working on documentation, remember to check against https://scipy.github.io/devdocs/index.html - this is the version of the documentation corresponding to the latest development version (aka what is merged on the main branch on github). The https://docs.scipy.org/doc/scipy/reference/ version might be outdated (corresponds to the latest release).

### How to Co-author commits
If you worked in a pair/group and want to know how to acknowledge multiple authors on the PR.  Find some helpful documentation [here](https://gist.github.com/lisawolderiksen/f9747a3ae1e58e9daa7d176ab98f1bad)

### Labelling commit messages
Commit messages should be clear and follow a few basic rules. Please try to label your commits with an indicative label.  A guide to best practice can be found [here](https://scipy.github.io/devdocs/dev/contributor/development_workflow.html#writing-the-commit-message)
 
### More useful links/resources:
- Melissa Weber's Talk: Sphinx for Python Documentation: https://youtu.be/tXWscUSYdBs
- Reshama Shaikh's intro to git: https://github.com/reshamas/git-intro-workshop
- A guide to making open source contributions, for first-timers and for veterans: https://opensource.guide/how-to-contribute/
- A guide to pair-programming: https://medium.com/@weblab_tech/pair-programming-guide-a76ca43ff389
- Mentored Sprints Community Handbook: https://mentored-sprints.netlify.app/

