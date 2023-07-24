# github actions test

This is a test folder to experiment with github actions.

Goal is that whenever someone makes changes to the repository, the website is regenerated.

See the embryonic website at work here: [pverkind.github.io/gh_actions_test](https://pverkind.github.io/gh_actions_test)

You can see the output reports of the github actions script on the "Actions" tab in your github repo

# setup

For this to work, you should:

1. enable GitHub Actions with the correct permissions:

* Under your repository name (gh_actions_test), click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
* In the left sidebar, click  Actions, then click General.
* scroll down to "Workflow permissions", select "Read and write permissions" and press "save".

2. enable GitHub Pages:

* Under your repository name, click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
* In the left sidebar, click  Pages
* Under "branch", choose "main", and click "save"
The content of the root folder of your repo is now served under <your_github_name>.github.io/gh_actions_test
(and because we have put the index.html file in the root folder, that will be displayed by default when you go to that page)

# Folder structure

```
|- .github/
|     |- workflows/
|     |     |- python_workflow.yml: script that runs on github server anytime something is changed to the repo
|     |- build_html.py : script that builds the website
|- data/ : folder that contains the witness text files
|- html/ : folder that contains the generated witness html pages
|- index.html: home page containing links to the witness html files
```

# to do

* add a condition to the workflow yml file that whenever the python file is changed, the whole data folder needs to be reconverted (that is, the python script should be called with "data" as its parameter).
* rename the python_workflow.yml to "build_website.yml"
* create a new workflow file called "new_release.yml", which will use the "on: workflow_dispatch" event to enable Kevin to create a new release version of the website manually (see https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch):
  - creates a new time-stamped folder that is a copy of the work-in-progress folder
  - creates a new index.html file in the root folder that diverts to the newest version
* create a workflow that creates a new release version every 3 / 6 months? 
