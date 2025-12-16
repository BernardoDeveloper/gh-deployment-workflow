# GitHub Deployment Workflow

The workflow starts by configurantion in the file .github/workflows/deploy.yml
In this file i set when has a new push on branch main start the execution from the workflow, to this need set this in the code:

```yml
on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]
```

After this setup, need set the permission to GITHUB_TOKEN this is used to workflow made the automatic process
And set the job configuration. To this need create the enviroment and in GitHub has some variables to use, example is `steps.deployment.outputs.page_url` and return the url set to this project
With this configuration can call all steps when has a new push on branch main. I call the functions from GitHub to valid the project and upload then, setting the all repository

```yml
jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          # Upload entire repository
          path: '.'
```

---

[Roadmap.sh project idea](https://roadmap.sh/projects/github-actions-deployment-workflow)
