+++
title =  "Git Work From Local Repository"
+++

<h1> <span style="color: #da1953">Git</span>work from local repository</h1>

Oct 30, 2022

---

<h2> <span style="color:#da1953">Ind</span>ex </h2>

- [Install Git](#SET)
- [Set up personal access token](#TOK)
- [Download And Update Repository](#UP)

<h2 id=SET> <span style="color: #da1953">Ins</span>tall Git </h2>

Install git from repository: `sudo apt install git`

<h2 id=TOK> <span style="color: #da1953">Ins</span>tall Personal Access Token </h2>

Log in to GitHub and navigate to the Settings page as shown below:

![Settings](/gitworkfromlocalrepository/settings.png)

Click on Developer Settings

![Dev Settings](/gitworkfromlocalrepository/devsettings.png)

Click on Personal Access Tokens

![Personal Access Token](/gitworkfromlocalrepository/pat.png)

Click on Generate new token

![Generate Access Token](/gitworkfromlocalrepository/generate.png)

Now type the name of the token and select the scopes, or permissions, you’d like to grant this token. Make sure you select *repo* to use your token to access repositories from the command line. Click Generate token at the bottom of the page.

![Key Settings](/gitworkfromlocalrepository/keysettings.png)

Now the key cna be used to upload and update the project on github.

![Key](/gitworkfromlocalrepository/key.png)



<h2 id=UP> <span style="color: #da1953">Dow</span>nload And Update Repository </h2>

**Step 1**

`git clone <REPOSITORY>`

e.g. `git clone https://github.com/Benwick921/benwick921.github.io.git`

Once downloaded the repository make your changes.

If you dont want *git* to create the folder with the same name of the  repository you can run the following command from an empty folder.

`git clone <url form web> .`

e.g. `git clone https://github.com/Benwick921/benwick921.github.io .`

**Step 2**

Add file content to the idex.

`git add .`

**Step 3**

Record changes to the repository.

`git commit -m "message"`

**Step 4**

Update remote refs along with associated objects.

`git push https://<GITHUB_ACCESS_TOKEN>@github.com/<GITHUB_USERNAME>/<REPOSITORY_NAME>.git`

Remember to replace <GITHUB_ACCESS_TOKEN>, <GITHUB_USERNAME>, <REPOSITORY_NAME> with your token, username and repository.

eg. `git push https://ghp***********************YC@github.com/Benwick921/Benwick921.github.io.git`

In case of upload error `-f` flag can be used.

