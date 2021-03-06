# The Reasoning and Learning Lab Website

[http://rl.cs.mcgill.ca/](http://rl.cs.mcgill.ca/)

This repo contains the **production build** of the new website redesign (November 2021). The previous website was hard to maintain as its a plain old html file. The new redesign should make website maintenance easy and can be done by anyone in the lab, directly from Github.

- Easy to maintain, as it uses Jekyll to generate webpages
- Easy to contribute, as you can just write markdown files
- Easy to update personal information, which can be made by just editing the `.yml` files
- Easy to deploy, as any PR merge will trigger remote build and push to our server

The website is powered by [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme, which is now increasingly used by many personal portfolios, labs and conferences. Jekyll and Github Actions automation allows us to have the following features:

- ✔️ Directly edit and update your information, even after graduating
- ✔️ No knowledge of html needed, just update your information in plain text yaml file
- ✔️ Long term minimum maintainance
- ✔️ Automatically builds and updates the website on any change
- ✔️ Publications page auto updates every week
- ✔️ Professors get dedicated landing pages

## Updating information

Updating information of students, professors and alumni is very easy, and can be done even through the Github web interface. All data resides in `_data/` folder in various `.yml` files. For each profile, you should first upload an image in `assets/img/` folder.

### Updating a professor/affiliate faculty information

Edit the `_data/professors.yml` file, and add the following information:

```yaml
- name: Doina Precup
  image: dprecup.jpg
  website: https://cs.mcgill.ca/~dprecup
  description: Reinforcement Learning, Reasoning and planning under uncertainty
  scholar:
  level: core
  bio: |
    Add a prof's bio here
  dblp: Link to DBLP RSS feed
  startyear: 2001
```

Add the required information. `level` tag accepts either `core` or `affiliate`, which adds the professor's profile in the correct subheaders in [Team page](http://rl.cs.mcgill.ca/team/).

#### Landing Page

Professors are very busy, so it is natural to not expect them to maintain their own students page regularly. Here, we make it super easy for a professor to maintain a list of students information for themselves! Specifically, each `core` professor gets their own dedicated landing page, which consists of their bio, students information, and course information. Any student having the prof in `supervised_by` field will be featured in this landing page, along with their degree. This page also features the list of alumni of each professor. Thus, any student can easily update their information here, which will be reflected in the website.

Professors can also update their course offerings directly to be reflected in the landing page and in the [courses]() page. To add/update course, we have a `_data/courses.yml` file which takes the following keys in a list item:

```yaml
 - name: "COMP-767 : Reinforcement Learning"
  website: http://cs.mcgill.ca/~dprecup/
  description: New course available for the Winter 2017 semester.
  active: false
  offered_by: Doina Precup
  semester: Fall 2020
```

If `active` set to `true`, the course will be featured as an "Active Course", else will be known as a "Past Course".

### Updating a student (postdoc/phd/msc/alumni)'s information

Edit the `_data/students.yml` file, and add the following information:

```yaml
- name: Koustuv Sinha
  image: ksinha.jpg
  website: https://cs.mcgill.ca/~ksinha4
  description: Natural Language Understanding, Systematicity & Logic in NLU, Dialog Systems # it could be research interests, or if alumni where you are now
  supervised_by: Joelle Pineau
  scholar:
  level: phd
```

Add the required information. `level` tag accepts `postdoc`, `phd`, `msc`, `alumni` for displaying profiles under the respective subheaders in [Team page](http://rl.cs.mcgill.ca/team/). For alumni, extra fields `grad_degree`,`grad_year` and `status` are required:

```yaml
- name: Ali Emami
  image: aliemami.webp
  website: http://www.cosc.brocku.ca/~aemami/
  status: Assistant Professor, Brock University
  scholar:
  level: alumni
  grad_degree: PhD
  grad_year: 2021
```

This configuration will hopefully make long term maintenance easier!

## Publications

We also maintain list of [publications](https://rl.cs.mcgill.ca/publications/) by RLLab Profs (core and affiliate). A [python script](/fetch_publications.py) is used to fetch and parse publications from our profs (thanks to the OG Pierre Luc for the initial version of this script!). To include a prof in the search list, ensure the data of the prof in `_data/professors.yml` contains the fields `dblp` and `startyear`, where `dblp` is the RSS permalink of the user from [DBLP](https://dblp.org/), and `startyear` is the year when the prof started their tenure in McGill. This script will be periodically executed by Github Actions (`schedule` workflow) to maintain an up to date list of our lab members.

## Contributing and Moderation

Since anyone can trivially update any information of the website through this repository, obviously it will be moderated. The website management team, along with volunteers, will be in charge of moderating changes in this repository. Specifically, this repository will be public, and anyone can submit a Pull Request (PR) of the change. After a light moderation (to make sure the data is correct), a member from the management team will merge the PR, which will result in updation of the website shortly.

Adding/updating information in this website is trivial. You don't even need to clone the repository in your machine, you can directly edit this website through Github and submit a Pull Request. Just navigate to the file (`_data/students.yml` for students, `_data/professors.yml` for Professors) and click "Edit this file" on the top-right (a pencil icon). Once you have added your information, create a pull request. Here is a [step-by-step guide](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files#editing-files-in-another-users-repository) on how to do so.

## Deploying

The website currently resides in [http://rl.cs.mcgill.ca/](http://rl.cs.mcgill.ca/). The build and deploy Github actions are in `.github/workflows/jekyll.yml`, which is heavily inspired from this [nice blog post](https://christianspecht.de/2020/05/03/building-and-deploying-a-jekyll-site-via-github-actions/).

## Contact persons

For bug reports, feature requests, and feedback, please contact the following persons in the lab (or in Mila Slack):

- Koustuv Sinha
- Martin Klissarov
