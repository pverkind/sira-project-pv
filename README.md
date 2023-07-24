# Sira project website

This is a prototype of a website for Kevin Jaques' Sira Project. 
It can be viewed here: [pverkind.github.io/sira-project-pv/](https://pverkind.github.io/sira-project-pv/)

The website is versioned: the index.html file in the root folder of the repository
will redirect to the latest released version (releases are dated: vYYYY-MM-DD).

The latest changes (since the latest release) are visible under 
[pverkind.github.io/sira-project-pv/work-in-progress](https://pverkind.github.io/sira-project-pv/work-in-progress)
External users should only use the released version, which is citable and does not change.

The goal is that Kevin can keep on working on his files and whenever he pushes his changes to GitHub,
the changes will be reflected in the work-in-progress page. When he's happy with the current state of the website
(or, every 6 months), he can create a new dated release. 

The GitHub Actions script that updates the website whenever a change is pushed to GitHub
also performs some consistency tests on the data. You can see the output reports (logs) of the GitHub Actions 
script under the "Actions" tab in the github repo. In the left-hand column, click "Build website" to see
a report for all website updates. Click on the label of the latest run of the "Build website" workflow,
then click "build-html" and then on "rebuild website". The log lists all the inconsistencies the script found
in the witness files; you can fix these manually in the witness files. 


# setup

For this to work, you should:

1. enable GitHub Actions with the correct permissions:

* Under your repository name (sira-project-pv), click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
* In the left sidebar, click  Actions, then click General.
* scroll down to "Workflow permissions", select "Read and write permissions" and press "save".

2. enable GitHub Pages:

* Under your repository name, click  Settings. If you cannot see the "Settings" tab, select the  dropdown menu, then click Settings.
* In the left sidebar, click  Pages
* Under "branch", choose "main", keep the default location as "root/"  and click "save"
The content of the root folder of your repo is now served under <your_github_name>.github.io/sira-project-pv
(and because we have put the index.html file in the root folder, that will be displayed by default when you go to that page)

# Folder structure

```
|- .github/
|     |- workflows/
|           |- build_website.yml: script that runs on github server anytime something is changed to the repo;
|                                 it uses the build_html.py script (in the root folder) to rebuild the website.
|- witness_data/ : contains the witness text files
|- homepage_data/ : contains markdown files for each section on the homepage. 
|                   When you create a new markdown file here, a new section will be added to the menu bar. 
|- work-in-progress/ : contains the generated witness html pages for the latest data
|     |- css/ : contains the css files that define the styling of the website
|     |- js/ : contains the javascript files that make the website interactive
|     |- ... : all html files of the website 
|- vYYYY-MM-DD/ : v for version, YYYY for year, MM for month, DD for day: stable releases of the website
|- images/ : contains all images needed for the website (photos of contributors, header image, funders' logos, ...)
|- meta/ : contains the Excel files with the metadata for the witness codes and bibliography
|- templates/ : contains the templates used to build the website
|- index.html: web page that sends the user to the latest release version of the website
|- build_html.py: the python script that builds the website
|- requirements.txt: a list of all Python libraries used by the Python scripts
|- README.md: this documentation file
```

# How to use this repository? (for Kevin)

* Anytime BEFORE you want to work on the texts on your computer, pull the latest changes from GitHub: 
  `git pull origin main`
* The witness files are in the witness_data folder: work on them there, and whenever you are ready, 
  push them to GitHub using these commands:
  - `git status`  (shows you all files that have changed)
  - `git add .`   (this collects all changes you made)
  - `git commit -m "(write a message describing what you changed here)"`  (record your changes in your local git repo)
  - `git pull origin main`  (make sure you have the latest changes from GitHub)
  - `git push origin main`  (this sends your changes to GitHub)

  Once you have pushed the changes, the [work-in-progress page](https://pverkind.github.io/sira-project-pv/work-in-progress) will be updated
  (this will take a couple of minutes; you can follow the progress in the Actions tab on the repo's GitHub page)
* If you want to change the descriptions on the website, open the relevant file 
  in the `homepage_data` folder. Anything you write here should be in 
  [markdown](https://www.markdownguide.org/basic-syntax/); this will be automatically
  converted into HTML by the script. Once you have finished updating the files, 
  push them to GitHub using these commands:
  - `git status`  (shows you all files that have changed)
  - `git add .`   (this collects all changes you made)
  - `git commit -m "(write a message describing what you changed here)"`  (record your changes in your local git repo)
  - `git pull origin main`  (make sure you have the latest changes from GitHub)
  - `git push origin main`  (this sends your changes to GitHub)

  Once you have pushed the changes, the [work-in-progress page](https://pverkind.github.io/sira-project-pv/work-in-progress) will be updated
  (this will take a couple of minutes; you can follow the progress in the Actions tab on the repo's GitHub page)

# TO DO: 

* create a new workflow file called "new_release.yml", which will use the "on: workflow_dispatch" event to enable Kevin to create a new release version of the website manually (see https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch):
  - creates a new time-stamped folder that is a copy of the work-in-progress folder
  - creates a new index.html file in the root folder that diverts to the newest version
* create a workflow that creates a new release version every 3 / 6 months? 
