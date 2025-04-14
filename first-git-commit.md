# Git installation problems (1st time installation)

Needed to get this repo working up and running on github from my local directory. But, had no idea on how to do it. To record the steps i took for this setup, I write the steps here.

## Steps towards the remote commit:

- Go to *~/path/to/journals*
- **git init** [this initializes the directory as a git repo]
- **git remote add origin** [link to the repo](https://github.com/shub-krishan208/journals.git)
- **git add .** [to add everything present to the repo]
- **git commit -m "commit message"**
- **git branch -M main** [the 'git init' make the branch name 'master' so we change it to 'main']
- **git push -u origin main** [finally the push request is sent to the repo]

## Problems faced:

1. When the repo is created online and the push request is sent locally, a merger clash occurs, where the files already in the repo and the newer files fight for existence. Here, **we're supposed to provide for a way to make the merger**.

   The options being, delete one and keep other or keep both. I needed to *keep both*. So, I first **pulled** the repo contents (using: **git pull origin main --rebase**), and then pushed back.

2. There was this authentication issue I faced while sending the push request, as it was my own repo,  I set up a PAT and tied it to the repo and used it for authentication (using an SSH key was also an option, but I *failed* to set it up properly :P).

   NOTE: The PAT key is only displayed once **while generation** after that, I **can't view** it again. So, must copy it somewhere safe.
