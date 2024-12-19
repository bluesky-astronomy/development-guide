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

**4. Set up relevant environment variables**

Required environment variables for each project are/will be documented in the readme file of every repository. 

> [!NOTE]  
> To work with a repository that requires setting the `BLUESKY_DATABASE` environment variable, you'll need to download the development copy of the database. Currently, the link lives in a pinned message in the #dev-discussion channel on the development Discord.


## Repository Structure

The **Astronomy on Bluesky** project consists of the following repositories:

| **Repository**          | **Description**                                                                                                                                    | **Branch protection?** |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `.github`               | Template things for the Bluesky-Astronomy organization.                                                                                            | Yes                    |
| `astro-ph-bots`         | A collection of bots that post new papers added to astro-ph to Bluesky.                                                                            | Yes                    |
| `astrobot`              | A bot that handles actions on the Astronomy feeds, like signups. It will also eventually include moderation and DM tools.                          | Yes                    |
| `astrofeed-lib`         | Common functions for working with the Astronomy feeds, including the database and feed spec.                                                       | Yes                    |
| `astrofeed-news-bot`    | A bot for posting news and updates about the Astronomy feeds.                                                                                      | Yes                    |
| `astrofeed-server`      | Flask web app for hosting the astronomy feeds.                                                                                                     | Yes                    |
| `astronomy-feeds`       | Python module for crawling the [Bluesky](https://bsky.app) firehose of posts and finding all that match criteria specified by the Astronomy feeds. | Yes                    |
| `BlueSky-Mastadon-CLI`  | Basic command-line-interface (CLI) scripts to post to BlueSky and Mastodon simultaneously.                                                         | Yes                    |
| `branding`              | Branding resources and logos for the Astronomy feeds.                                                                                              | Yes                    |
| `development-guide`     | This guide!                                                                                                                                        |                        |
| `dm-bouncer`            | A direct message 'bouncing' service for limited group DMs. Intended for communication for moderators on the Astronomy feed.                        | Yes                    |
| `Galaxy-Zoo-Poster-Bot` | A bot to post an image of a galaxy from the Galaxy Zoo archives every hour on BlueSky.                                                             | Yes                    |
| `rules`                 | Rules which anyone posting to the Astronomy feeds must follow.                                                                                     | Yes                    |
| `scripts`               | Scripts and notebooks to do various little jobs, like database maintenance or making plots.                                                        |                        |
| `website`               | The astronomy.blue website.                                                                                                                        | Yes                    |


## Workflows and Standards

- **Code Style**:
  - For now, recommend following community-supported standards and best practices for each language. For example:
    - Python: [PEP 8 -- Style Guide for Python Code](https://peps.python.org/pep-0008/)
    - Python: Usage of Type Hints on variable definition. For example:
      - num_files: int
      - user_name: str
    - Typescript: [Airbnb style guide](https://github.com/airbnb/javascript)
  - Formal guidance for code style coming soon!
- **Branching Strategy**:
  - Use the `feature-`, `bugfix-`, `hotfix-`, and `chore-` prefixes for branches.
  - Main branch: `main`.
  - The `main` branch has branch protections on most repositories (see above table.) Commits to main will require approval.
- **Code Reviews**:
  - All code must go through a pull request (PR) process.
  - Assign at least one reviewer.
- **Testing**:
  - Unit tests are required (where possible) for all new features.
  - Run tests locally before submitting a PR.
- **CI/CD Pipeline**:
  - Coming soon!


## Resources and Support

### Astronomy on Bluesky
- [GitHub org that all code lives in](https://github.com/bluesky-astronomy)
- [The current to-do list](https://github.com/orgs/bluesky-astronomy/projects/1/views/1)
- [Our stub website](https://astronomy.blue) that needs an overhaul...
### Useful documentation
#### AT Protocol
- [Docs for the Python SDK](https://atproto.blue)
- [Official protocol docs](https://atproto.com)
- [Bluesky's source code](https://github.com/bluesky-social/atproto)
#### Other libraries
- [peewee](https://docs.peewee-orm.com), our database ORM
#### Useful 3rd party tools
- [edavis.dev's charts of Bluesky activity](https://bskycharts.edavis.dev/bluesky-day.html)
- [Jaz's stats page](https://bsky.jazco.dev/stats)
- [Bluesky handle debug tool](https://bsky-debug.app/handle?handle=astronomy.blue) (can also look up DIDs)
- [Clearsky search tool](https://bsky.thieflord.dev/) (currently down as of 19th Dec.)
- [Searchable list of all firehose commits](https://atproto.tools/) (currently down as of 22nd Nov.)
