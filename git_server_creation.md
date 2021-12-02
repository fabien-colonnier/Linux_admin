# Description of the use of the git server

The working tree is made which his user having its own folder containing its own repositories.
If multiple users are working on the same project, it is still possible but at least the main maintainer is known.

If you want to make sure no one else can push to your repo change the ownership with:
`chown -R <your_username>:<your_username> <path_to_repository>/ `

default is:
`chown -R <your_username>:gitusers <path_to_repository>/`

In general, please, users should be mindful and don't mess up the others repositories.

for more information see: https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server

## Add a ssh public key
It is useful to avoid to key the password each time you do any update.
On you local machine, create the ssh key and add it to the authorized_keys.
```
cd ~/.ssh/
ssh-keygen -f <key_name> 
```
In case the key is not added to the ssh agent. You should do:
`ssh-add ~/.ssh/<key_name>`

Upload the public key to the server

`cat ./<key_name>.pub | ssh <your_username>@host "cat >> ~/.ssh/authorized_keys"`

## Create a new repository

#### On the server

First, you need to be logged as the git user (git)
`ssh <your_username>@host `
or directly log on the server

Creation of the folder for the new repo
` mkdir -p /git_server_path/<your_username>/<your_new_repo_name> `
`cd  /git_server/<your_username>/<your_new_repo_name>`

Init the empty git repository
`git init --bare`

#### On your computer

init the folder containing your project and do the first commit
```
cd <myproject>
git init
git add .
git commit -m 'initial commit'
git remote add origin git@host:/git_server_path/<your_username>/<your_new_repo_name>
git push origin master
```

#### Optional

Create a .gitignore file containing the file of the file you don't want to commit
see for more details
https://www.atlassian.com/git/tutorials/saving-changes/gitignore

useful gitignore repo
https://github.com/github/gitignore

#### To duplicate a repo on another machine
```
git clone <your_username>@host:/git_server_path/<username>/<repo_name>
```
