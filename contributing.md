# Documentation Contributing Guide

We welcome contributions from all users and the community. By contributing, you agree to the [Percona Community code of conduct](https://percona.community/contribute/coc/). Thank you for deciding to contribute and help us improve the [Percona XtraBackup documentation](https://docs.percona.com/percona-xtrabackup/).

You can contribute to the documentation in the following ways:

- [Add a topic](#add-a-topic)
- [Request a doc change through a Jira issue](#request-a-doc-change-through-a-jira-issue)
- [Contribute to the documentation yourself](#contribute-to-documentation-yourself)

## Add a topic

In the [Percona Product Documentation category](https://forums.percona.com/c/percona-product-documentation/71) in the Percona Community Forum, select New Topic. Complete the form and select Create Topic to add the topic to the forum.![Create a topic](docs/_static/new-topic.png "Create a topic")

## Request a doc change through a Jira issue

**Request a doc change through a Jira issue**. If you’ve found a doc issue (a typo, broken links, inaccurate instructions, etc.) create a Jira ticket to let us know about it if you would rather not [contribute to the documentation yourself](#contribute-to-documentation-yourself).

- Open the [Jira issue tracker](https://jira.percona.com/projects/PXB/issues) for the doc project.
- Sign in (create a Jira account if you don’t have one) and click **Create** to create an issue.
- In the following fields, describe the issue:
    - In the Summary, provide a brief description of the issue
    - In the Description, provide more information about the issue, along with a Steps To Reproduce section, if needed
    - In the Affects Version/s field, if you know this issue affects multiple versions, please enter the version numbers. It is OK to add the version number with an ".x" (such as ``8.0.x``) if you don't know the exact version that must be updated.

## Contribute to documentation yourself

There is the **Edit this page** link that leads you to the source file of the page on GitHub. There you make changes, create a pull request that we review and add to the doc project. For details how to do it, read on.

To contribute to documentation, learn about the following:

- [Markdown](https://www.mkdocs.org/) 
- [MkDocs](https://daringfireball.net/projects/markdown/) 
- [git](https://git-scm.com/) and [GitHub](https://guides.github.com/activities/hello-world/)
- [Docker](https://docs.docker.com/get-docker/). It allows you to run MkDocs in a virtual environment instead of installing it and its dependencies on your machine.

There are several active versions of the documentation. Each version has a branch in the repository named accordingly:

- 2.4
- 8.0

The `.md` files are in the ``docs/`` directory. 

### Edit documentation online using GitHub

1. Click the **pencil** icon next to the page title to edit the document. The source ``.md`` file of the page opens in GitHub editor in your browser. If you haven’t worked with the repository before, GitHub creates a [fork](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) of it for you.

2. Edit the page. You can check your changes on the **Preview** tab.

3. Commit your changes.

	 - In the *Commit changes* section, describe your changes.
	 - Select the **Create a new branch for this commit and start a pull request** option
	 - Click **Propose changes**.

4. GitHub creates a branch and a commit for your changes. It loads a new page on which you can submit a pull request to Percona. The page shows the base branch - the one you offer your changes for, your commit message and a diff - a visual representation of your changes against the original page. At this time you can make a last-minute review. When you are ready, click the **Create pull request** button.
5. Someone from our team reviews the pull request. They may make a comment or they may approve it. The approved pull request is merged into documentation when the next version of Percona XtraBackup is released. 

### Edit documentation locally

This option is for users who prefer to work from their computer and/or have the full control over the documentation process.

The steps are the following:

1. Fork this repository

2. Clone the forked repository to your machine:

    ```sh
    git clone git@github.com:<your_GitHub_account_name>
    ```

3. Change the directory to ``pxb-docs/docs`` and add the remote origin repository:

    ```sh
    git remote add origin git@github.com:percona/pxb-docs.git
    ```

4. To be sure that you have the latest changes, checkout the appropriate branch and pull the latest changes from origin

    ```sh
    git checkout 8.0 && git pull origin 8.0
    ```
    Make sure that your local branch and the branch you merge changes from are the same. So if you are on ``8.0`` branch, pull changes from ``origin 8.0``.

5. Create a separate branch for your changes

    ```sh
    git checkout -b <my_changes>
    ```

6. Make changes in the documentation
7. Add the changed files

    ```sh
    git add <changed files>
    ```
8. Commit your changes

    ```sh
    git commit -m 'Fixed typing error in <document name>'
    ```
9. Open a pull request to Percona

    ```sh
    git push <my repo> <my_changes>
    ```

### Building the documentation

To verify how your changes look, generate the static site with the documentation. This process is called *building*. You can use the following methods:
- [use Docker](#use-docker)
- [build locally](#build-locally)

#### Use Docker

1. [Get Docker](https://docs.docker.com/get-docker/)
2. We use [our Docker image](https://hub.docker.com/repository/docker/perconalab/pmm-doc-md) to build documentation. Run the following command in the ``docs`` directory:

    ```sh
    docker run --rm -v $(pwd):/docs perconalab/pmm-doc-md mkdocs build
    ```
    If Docker can't find the image locally, it first downloads the image, and then runs it to build the documentation.

3. Go to the ``site/`` directory and open the ``index.html`` file to see the documentation.

   If you want to see the changes as you edit the docs, use this command instead:

   ```sh
   docker run --rm -v $(pwd):/docs -p 8000:8000 perconalab/pmm-doc-md mkdocs serve --dev-addr=0.0.0.0:8000
   ```

   Wait until you see the message `INFO    -  Start detecting changes`, then enter `0.0.0.0:8000` in the browser's address bar. The documentation automatically reloads after you save the changes in source files.

#### Build locally

1. Install [pip](https://pip.pypa.io/en/stable/installing/)
2. Install [MkDocs](https://www.mkdocs.org/).
3. While in the root directory of the doc project, run the following command to build the documentation:

    ```sh
    mkdocs build
    ```
4. Go to the ``site`` directory and open the ``index.html`` file in your web browser to see the documentation.
5. To automatically rebuild the documentation and reload the browser as you make changes, run the following:
   
   ```sh
   mkdocs serve
   ```
   Wait until you see the message `INFO    -  Start detecting changes`, then enter `0.0.0.0:8000` in the browser's address bar. 

## PDF

To create the PDF version of the documentation, use the following command:

* With Docker:

    ```sh
    docker run --rm -v $(pwd):/docs -e ENABLE_PDF_EXPORT=1 perconalab/pmm-doc-md mkdocs build -f mkdocs-pdf.yml
    ```

* Without:

    ```sh
    ENABLE_PDF_EXPORT=1 mkdocs build -f mkdocs-pdf.yml
    ```

The PDF is in `site/_pdf`.

## Repository structure

The repository includes the following directories and files:

- `mkdocs-base.yml` - the base configuration file. It includes general settings and documentation structure.
- `mkdocs.yml` - configuration file. Contains the settings for building the docs with Material theme.
- `mkdocs-pdf.yml` - configuration file. Contains the settings for building the PDF docs.
- `docs`:
  - `*.md` - source markdown files.
  - `_static` - images, logos and favicons
  - `css` - styles
  - `js` - Javascript files
- `_resource`:
   - `templates`:
     - ``styles.scss`` - Styling for PDF documents
   - `theme`:
      - `main.html` - the layout template for hosting the documentation on Percona website
   - `overrides` - the folder with the customized templates
- `site` - this is where the output HTML files are put after the build