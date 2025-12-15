# Developer Onboarding Guide for Astronomy on Bluesky

<img src="https://raw.githubusercontent.com/bluesky-astronomy/branding/refs/heads/main/png/astro-transparent.png" width="200" alt="Astronomy on Bluesky logo">

**Welcome to the Astronomy on Bluesky development team! 🎉**

This guide is your starting point for getting up to speed with the project. It provides all the
resources, tools, and information you need to hit the ground running.


## About the Project

**System Architecture:**

<img src="architecture.jpg" width="800" alt="Astronomy on Bluesky architecture diagram">


## Getting Started

Follow these steps to get started:

1. **Request Access**: Ensure you have access to the required resources.
   - [ ] Bluesky account
   - [ ] Added to github Astronomy on Bluesky org
   - [ ] Added to Bluesky Devs Discord
2. **Set Up Your Environment**: Follow the [Development Environment Setup](#development-environment-setup) instructions to configure your local machine.
3. **Explore the Codebase**: Start with the [Repository Structure](#repository-structure) section for an overview of the code organization.
4. **Start Your First Task**: [Pick a First Task](https://github.com/orgs/bluesky-astronomy/projects/1) to familiarize yourself with the project and workflow.



## Development Environment Setup

### Python projects

**1. Install the [uv python package manager](https://docs.astral.sh/uv/):**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**2. Clone the repository you'd like to work on - either with git:**

```bash
git clone <repo_url>
```

**or the [GitHub CLI:](https://cli.github.com/)**

```bash
gh repo clone bluesky-astronomy/<repo_name>
```

**3. Navigate into the repo and initialize a virtual environment with uv:**

```bash
uv sync
```

**4. Install PostgreSQL**

Many services require a running PostgreSQL development database to run locally. Detailed instructions are in [this file](https://github.com/bluesky-astronomy/development-guide/blob/main/PostgreSQLHowTo.pdf). You will also need to download a copy of the development database - for now: ask Emily. (As of December 2025, we're hoping to improve this step soon - sorry!)


**5. Set up relevant environment variables**

Required environment variables for each project are/will be documented in the readme file of every repository. 

> [!NOTE]  
> To work with a repository that requires setting the `BLUESKY_DATABASE` environment variable, you'll need to download the development copy of the database. We're in the process of updating how this gets shared and downloaded (December 2025); for now, please ask Emily for a copy.


### Svelte projects (for now: just the website)

**1. Install npm**

We recommend first installing [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating) to manage node.js installs. Then, install the latest LTS release of npm with

```bash
nvm install --lts
```

```bash
nvm use --lts
```


**2. Install required dependencies**

Instructions may depend on the project, but this is usually as simple as doing `npm install` in the folder.


**3. Start development server**

The following `npm` commands are useful:

- `npm run dev`: runs a development copy of the server locally.
- `npm run build`: performs a test build of the site/app. Useful to test build pipeline.
- `npm run preview`: previews the site/app locally from build artifacts. Useful to test build pipeline.

> [!NOTE]  
> Some parts of the website require connection to the Flask backend. By default, in dev mode, the website is configured to connect to a **locally running** Flask server. You will need to go through the Python setup steps above, get a dev database running, set the dev environment variable, and then do `./run_server` in the astronomy-feeds folder to start a Flask server. (See [this guide](https://github.com/bluesky-astronomy/astronomy-feeds?tab=readme-ov-file#astrofeed_server)).


## Repository Structure

The **Astronomy on Bluesky** project consists of the following (main) repositories:

| **Repository**          | **Description**                                                                                                                                    | **Branch protection?** | **Private?** |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------ |
| `.github`               | Template things for the Bluesky-Astronomy organization.                                                                                            | Yes                    |              |
| `astronomy-feeds`       | MAIN MODULE. Includes code for the firehose, database spec, a moderation bot, and a Flask server to serve the feeds to users.                      | Yes                    |              |
| `branding`              | Branding resources and logos for the Astronomy feeds.                                                                                              | Yes                    |              |
| `development-guide`     | This guide!                                                                                                                                        |                        |              |
| `devops`                | Devops resources, including Ansible configurations for deploying servers.                                                                          | Yes                    | Yes          |
| `dm-bouncer`            | A direct message 'bouncing' service for limited group DMs. Intended for communication for moderators on the Astronomy feed.                        | Yes                    |              |
| `Galaxy-Zoo-Poster-Bot` | A bot to post an image of a galaxy from the Galaxy Zoo archives every hour on BlueSky.                                                             | Yes                    |              |
| `moderation-guide`      | A guide for the feed moderators, with instructions about things like what to moderate (and how.)                                                   | No                     |              |
| `rules`                 | Rules which anyone posting to the Astronomy feeds must follow.                                                                                     | Yes                    |              |
| `scripts`               | Scripts and notebooks to do various little jobs, like database maintenance or making plots.                                                        |                        |              |
| `website`               | The astronomy.blue website.                                                                                                                        | Yes                    |              |


## Workflows and Standards

- **Code Style**:
  - For now, recommend following community-supported standards and best practices for each language. For example:
    - Python: [PEP 8 -- Style Guide for Python Code](https://peps.python.org/pep-0008/)
    - Python: Run code through [Ruff](https://docs.astral.sh/ruff/)
    - Python: Usage of Type Hints on variable definition. For example:
      - num_files: int
      - user_name: str
    - JavaScript/Typescript: [Airbnb style guide](https://github.com/airbnb/javascript)
- **Branching Strategy**:
  - Use the `feature-`, `bugfix-`, `hotfix-`, and `chore-` prefixes for branches.
  - Main branch: `main`.
  - The `main` branch has branch protections on most repositories (see above table.) Commits to main will require approval.
- **Code Reviews**:
  - All code must go through a pull request (PR) process.
  - Assign at least one reviewer.
- **Testing**:
  - Unit tests are required (where possible) for all new features.
  - On the team, Vince has the most experience with setting up unit tests in the astronomy-feeds repo.
  - Run tests locally before submitting a PR.
- **CI/CD Pipeline**:
  - More coming soon! For now, the astronomy-feeds repo is checked for style with ruff on all PRs.


## Resources and Support

### Astronomy on Bluesky
- [GitHub org that all code lives in](https://github.com/bluesky-astronomy)
- [Development plan (is always the pinned issue)](https://github.com/bluesky-astronomy/astronomy-feeds/issues)
- [Our website](https://astrosky.eco)
### Useful documentation
#### AT Protocol
- [Docs for the Python SDK](https://atproto.blue)
- [Official protocol docs](https://atproto.com)
- [Bluesky's source code](https://github.com/bluesky-social/atproto)
- [A nice introductory talk about AT Protocol](https://www.youtube.com/watch?v=F1sJW6nTP6E)
#### Other libraries
- [peewee](https://docs.peewee-orm.com), our database ORM
- [Svelte/SvelteKit](https://svelte.dev/), our frontend framework of choice for web apps
#### Useful 3rd party tools
- [Bluesky handle debug tool](https://bsky-debug.app/handle?handle=astronomy.blue) (can also look up DIDs)
- [Explore the records on any Bluesky PDS](https://pdsls.dev/)
- [Clearsky search tool](https://bsky.thieflord.dev/) (can look up various things)
- [Look up different AT Protocol lexicons](https://lexidex.bsky.dev/)
- [edavis.dev's charts of Bluesky activity](https://bskycharts.edavis.dev/bluesky-day.html)
- [Jaz's stats page](https://bsky.jazco.dev/stats)
- [Searchable list of all firehose commits](https://atproto.tools/) (down as of 22nd Nov. 2024)
