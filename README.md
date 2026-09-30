# Technical Assessment

## Introduction

This project provides an opportunity to demonstrate your expertise in data engineering using a real-world dataset.

Imagine yourself as a successful (and rich) data engineer seeking to reinvest your earnings in Amsterdam's property market for passive income. Your objective is to purchase houses and apartments, which you plan to lease either through long-term agreements on Kamernet or short-term listings on Airbnb.

As a skilled data engineer, you have already collected a dataset containing house locations and nightly prices from Airbnb and a second dataset from Kamernet.

### Goal of the Assessment

The aim is to identify postcodes with investment potential and determine whether renting properties long-term through Kamernet or via Airbnb would be more profitable.

## Product Development

If you are applying for a non-engineering position:

- Create a conceptual design of how the implementation looks like (either components or process)
- Create a business case
- Create a roadmap with milestones how you would deliver this implementation with a team of engineers
- Create a storyline based on the above input to convince the customer to invest

## Engineering Deliverables

If you are applying for an engineering role, you must at minimum build one or more data pipelines that:

- Ingest rental data scraped from Kamernet (`./data/rentals.json`)
- Ingest data from Airbnb (`./data/airbnb.csv`)
- Clean both datasets
- Identify and address any missing or improper data by designing (and implementing if time permits) a backfill
  strategy
- Calculate potential revenue per property and per postal code for both rental and Airbnb sources
- Follow the principles of the [Medallion Architecture](https://www.databricks.com/glossary/medallion-architecture#:~:text=A%20medallion%20architecture%20is%20a%20data%20design%20pattern,%28from%20Bronze%20%E2%87%92%20Silver%20%E2%87%92%20Gold%20layer%20tables%29.)

The following deliverables are expected as part of the project:

- Exploratory notebooks with data validation checks (placed in the `./scratch` folder)
- Notebooks containing your pipeline implementation (located in the `./notebooks` folder)
- Libraries or buildable packages for your pipeline (stored in `./src/<package_name>`)
- Unit tests for your pipeline (included in the `./tests` folder)
- Documentation for your pipeline (documented in the `README` and `./docs` folders) - **explain the why, not the how**
- Export of datasets produced by your pipeline, formatted as Parquet files (placed in `./data/output`)
- Pipeline job configurations (included in the `./resources` folder)
- Workspace and repository access for the reviewers (see [Sharing your work with the reviewers](#sharing-your-work-with-the-reviewers))

We highly recommend using Databricks, you can set up a [free trial for professional use following Express Setup](https://signup.databricks.com/) or [Databricks Free Edition](https://www.databricks.com/learn/free-edition). However, we are primarily interested in understanding how you work, so feel free to pick a tool with which you are most comfortable—whether it’s a local PySpark instance, or a cloud service. Explain your reasoning. If you go with Free Edition, see [Using Databricks Free Edition](#using-databricks-free-edition) below for setup, its limits, and how to share the result with us.

Save everything in a private Git repository and share it with us. Deliver a clean repository: remove any redundant files, replace our README with your own, and provide clear instructions for building and running your project. If unsure how to structure your repository, we recommend starting with our [RevoData Declarative Automation Bundle Templates](https://github.com/revodatanl/revo-dabs). We expect you to spend 3-4 hours on the assessment, so apply your best judgment when prioritizing tasks.

### Stretch Goals

Following are a number of stretch goals of increasing difficulty that will give us an idea of how far you can go. We **do not expect** that you will be able to achieve all of these in the given time, so pick and choose whatever suits you best. It is preferable to focus on a complete and high-quality initial assessment rather than getting lost achieving these goals.

#### Level 1 / Engineer

- [ ] Build a CI/CD pipeline that deploys your data pipeline
- [ ] Run tests in your CI/CD pipeline
- [ ] Use pre-commit hooks to ensure code quality

#### Level 2 / Artist

- [ ] Build a visualization or dashboard displaying potential revenue per postcode (rental and Airbnb)
- [ ] Create diagrams of the data flows and of your CI/CD pipeline

### BONUS

#### Level 3 / Future-Proof

- [ ] Use Lakeflow Spark Declarative Pipelines (SDP) to build your pipelines
- [ ] Use expectations (if using SDP) or another framework (if not), to ensure data quality
- [ ] Deploy your pipeline using Declarative Automation Bundles

#### Level 4 / over 9000

- [ ] Load the data from `rentals.json` one record at a time with streaming ingestion
- [ ] Update the gold layer table(s) in real time as new streaming data arrives

#### Level 5 / 10x Developer

- [ ] Use the `./data/geo/post_codes.geojson` geographic dataset to enrich the Airbnb data with missing postcodes
- [ ] - or - Query an external API such as [public.opendatasoft.com](https://public.opendatasoft.com/explore/dataset/georef-netherlands-postcode-pc4/api/) to fill in the missing postcodes using a UDF
- [ ] Use the `./data/geo/amsterdam_areas.geojson` geographic dataset for your visualization

## Using Databricks Free Edition

[Databricks Free Edition](https://www.databricks.com/learn/free-edition) is enough to complete this assessment end to end: Unity Catalog, serverless compute, Lakeflow jobs and declarative pipelines, dashboards, Git folders and Databricks Asset Bundles are all available, and unlike the Express Setup trial it does not expire. Sign up, create your workspace, and work out the setup from the Databricks documentation, getting from an empty workspace to a deployed pipeline is part of what we are assessing.

A few characteristics of Free Edition are worth knowing _before_ you design your solution, because they will influence your choices:

- Compute is serverless only — there are no clusters to configure.
- There are quotas on concurrent job tasks, on active pipelines per type, and on SQL warehouse size.
- Only Python and SQL are supported.
- There is no account console; everything is administered from inside the single workspace.
- Outbound internet access is restricted by default, which matters both for calling external APIs and for tooling that downloads dependencies at deploy time.

The [Free Edition limitations](https://docs.databricks.com/aws/en/getting-started/free-edition-limitations) documentation has the authoritative list. We are not looking for you to beat the quotas: if one of them forces a design compromise, tell us what you did instead and why.

## Sharing your work with the reviewers

As part of the deliverable, you should ensure that we can access and review what you have built, including the underlying code.

Once the assessment has been finalized, you will receive instructions regarding the email addresses of the individuals to whom you should provide access to the relevant GitHub repository and Databricks workspace.

Concretely, we expect:

1. **Workspace access.** Reviewers are added as users of your Free Edition workspace. Note that Free Edition lets a workspace admin add users but not remove them again, so add only these two addresses.
2. **`CAN_MANAGE` on every asset bundle resource.** Jobs, pipelines, dashboards and the bundle's workspace folder. Prefer declaring this in your bundle configuration over clicking through the UI — it is reproducible, it is reviewable, and it is redeployed with the rest of your code. Tell us which target you deployed if it is not the default one.
3. **Access to the data.** Workspace permissions do not cover Unity Catalog objects; the catalog and schemas holding your bronze, silver and gold tables need their own grants.
4. **GitHub access.** The repository stays private; please add reviewers as collaborators with a role that lets them see the settings and CI runs as well as the code. Ask us for their GitHub handles if you do not have them.

Also make sure the repository actually contains everything: the bundle configuration, the notebooks, the `src` package, the tests, the Parquet exports, the docs, and the Markdown export of your AI tool session(s).

### Access checklist

- [ ] Added as the assessement reviewers to the Databricks workspace
- [ ] Reviewers have `CAN_MANAGE` on every asset bundle resource, applied through the bundle and redeployed
- [ ] Reviewers have grants on the catalog/schemas holding your bronze, silver and gold tables
- [ ] Reviewers are collaborators on the private GitHub repository
- [ ] The workspace URL and the repository URL are shared with us by email

## Review

Once you have completed this project, we will review it together. We are paying special attention to what you did or how you approached the pipeline logic and the challenges you addressed when issues arose. With the data provided, we expect some challenges, so we encourage creative workarounds and proactive measures.

As a note on using AI tools (ChatGPT, Copilot, etc.), we encourage you to use these tools to enhance your productivity. However, please remember that you are 100% responsible for the code you submit. You need to be able to explain how the code works and discuss the pros and cons of your implementations.

We also require you to submit a (Markdown) export of the AI tool session conversation(s) that you conducted while completing this assignment, to better understand your working process.

Please do **not** use AI assistants in any way during the interview. We want to assess your technical skills, problem-solving abilities, and communication skills. Additionally, we want to evaluate your ability to clearly and concisely explain your thoughts.

**Good luck, and see you on the other side!**
