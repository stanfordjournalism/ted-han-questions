# Instructions for the Computational Journalism class

By Monday evening, May 15, please have written at least 3 questions in the question section of this repo's [README.md](README.md)

- Use proper Markdown formatting to add to the unordered list of questions.
- Add your **initials** to the end of each question. Put your initials in *italics*.

This is kind of a way to get you more acquainted with the flow of collaborative editing/development using a system like Github. Try to avoid editing the file with your web browser.

Instead, try the add/commit/push/pull process with either:

- [The Github Desktop Client](https://help.github.com/desktop/guides/getting-started/)
- [Using your system command line](https://help.github.com/articles/adding-a-file-to-a-repository-using-the-command-line/)

# Fun with git and Github

Github is a fantastic service, one that has had a huge impact on the way we code and collaborate today. But it will also feel needlessly complicated until you realize that its easier and safer than the way you used to backup and share files and projects. One particular challenge we face is that for this class, we don't have to use many of Github's features (e.g. forking, branching) to do what we need, but you'll probably stumble across those terms in other tutorials and get needlessly confused.

So I've tried to make a straightforward list of the git/Github things we'll actually use. In past years I've written and rewritten tutorials on how to use Github. Not going to guarantee that they'll be crystal-clear for you:

- http://www.compciv.org/recipes/devops/git-and-github-setup/
- http://www.compciv.org/guides/devwork/setting-up-github-and-cli-operations/


## Using the Github desktop client

I don't use the Github desktop client because I'm more comfortable with typing things out than pointing-clicking buttons. That said, if you're new to the command line, by all means, use the [Desktop Client](https://help.github.com/desktop/guides/getting-started/). I find the interface hard to understand and explain, but you should run into fewer obscure-sounding error messages...


## The command-line process

Here are all the steps to record the changes you make to a repo and then to push those changes to the Github repo:

```sh
$ git add README.md
$ git commit -m "made a change to readme"
$ git push origin master
```

Since more than once person is collaborating on this repo, before you make changes, run `git pull` to get the latest changes from Github's repo to your cloned repo:


```sh
$ git pull origin master
```


### Cloning the repo

If you are using your command-line, this is how you make a clone of the repo to which you also have the rights to `push` changes:

```sh
$ git clone git@github.com:stanfordjournalism/ted-han-questions.git
```

This should create a subdirectory named `ted-han-questions` relative to wherever you ran the command. You should only have to do this once. Unless you delete the folder, then you can clone it again.

Change into the subdirectory with:

```sh
$ cd ted-han-questions
```

Make and save a change to your copy of the `ted-han-questions/README.md` file (using Atom text editor is fine).

### git-add

https://git-scm.com/docs/git-add



To begin the process of adding that change to our *repo's history*, we use the `git add` command; the command below tells git to "notice" (or stage) the latest changes you've made to the `README.md` file:

```sh
$ git add README.md
```

### git commit

https://git-scm.com/docs/git-commit

We then use the `git commit` command to record these changes as part of the repo history; the `-m` flag is shorthand for the *message* that you use to describe the commit to someone else who sees it:

```sh
$ git commit -m 'whatever d00d'
```

### git push

The whole point of git is that everyone/anyone can clone a repo and make changes and have their own copy and history of the repo. But generally, as collaborators, we want a unified code base. This is one of Github's core purposes, to act as a centralized repo from which all updates/changes are propogated.

We can `git add` and `git commit` all we want. But until we do a `git push`, our changes aren't added to the Github version of the repo:

```sh
$ git push origin master
```

This says to push your repo's commits to the repo that is specified as being the `origin`, and specifically, to the `master` branch.

If you cloned the repo correctly onto your own computer, you can run the following command:

```sh
$ git remote show origin
```

And it will (or should) tell you that the address/URL of the origin repo is:

    git@github.com:stanfordjournalism/ted-han-questions.git


# Git conflicts

It is inevitable that when more than one person tries to make edits and then push them to the "origin" repo, that a conflict will occur. You may have seen this kind of thing when trying to collaboratively edit a Word or Google Doc. 

It's not much different here, except the error messages are much scarier.

The most common error message will come when you're trying to push your changes to the remote server, but someone else has made changes to the origin/master Github repo between the time of your previous pull/clone, and now, as you're trying to push your version of the repo:

```sh
$ git add .
$ git commit -m 'tree question'
```

Again, add/commit does nothing to the master repo, so you should not have an error at this point. But, when it comes time to `push`:

```sh
$ git push 

To git@github.com:stanfordjournalism/ted-han-questions.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:stanfordjournalism/ted-han-questions.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
The step to hopefully fix things is in one of the "hints"; run `git pull`:

```sh
$ git pull
```

Depending on how your system is set up, you'll be sent to a bizarre text editor in which nothing makes sense. If you really care, you can start with this [StackOverflow question](http://stackoverflow.com/questions/13507430/git-commit-in-terminal-opens-vim-but-cant-get-back-to-terminal); otherwise, you should be able to move on by typing in these keys in this exact order:

        :wq


Git has a smart algorithm for figuring out if the two different versions of a conflicted file can be automatically resovlved. Which they usually can be in the common case where one person has added files to the top of a file, and the other person has made some changes to the end of the file.

Running `git pull` with automatically resolved conflicts will look like this:

```sh
$ git pull
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 6 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.
From github.com:stanfordjournalism/ted-han-questions
   3eddbed..cf22cd4  master     -> origin/master
Auto-merging README.md
Merge made by the 'recursive' strategy.
 README.md       |   2 +
 instructions.md | 119 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 2 files changed, 121 insertions(+)
 create mode 100644 instructions.md
 ```


Now run git push:

```sh
 $ git push
Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 737 bytes | 0 bytes/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To git@github.com:stanfordjournalism/ted-han-questions.git
   cf22cd4..383216e  master -> master
```   

### Unresolved conflicts in git

Every once in awhile, changes made by different users cannot be auto resolved. For example, consider a file that has this line:

```
The quick brown fox jumped over the lazy dog
```

User A moves some adjectives around on their version of the file

```
The lazy fox jumped over the quick brown dog
```

But User B decides to make the split the original line into modern poetry, but without changing the order of the words:

```
The quick 
   brown fox 
   jumped
over
   the lazy
                    dog
```

No matter which person pushes their changes first, the second person is going to be told that Git can't automatically resolve these changes. What you'll end up having to do, as the user slowest to the push, is to edit your copy of the file by hand and recommit it. More info here: 

https://githowto.com/resolving_conflicts

Please email me or contact me on Slack (@dannguyen at newsnerdery.slack.com) if you run into issues. Don't waste more than few minutes trying to debug git error messages, just wait for me to get back to you.

But above all, please do not use `git push --force` no matter what you've read on the Internet about it.







