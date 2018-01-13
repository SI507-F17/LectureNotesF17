# SI 507 | Lecture 8 | October 25, 2017 | Complex Git Version Control, Development Processes

# Admin

- Small assignment today
- Partner assignment to start today
- Small assignment in section, plus time to finish the other thing if you don’t have time today
- You can see the assignment as Project 4 - Git on Canvas

Any questions?

# Git and version control review

To review what we’ve gone over at least a bit so far…


## Git version control & connections to GitHub


- Create a repository on your own computer, with `git init`
- Or, fork a repository to your own account — create a copy — and clone it to your own computer `clone`
- Push data in a local git repository to a **GitHub repo** — a place on the internet, accessible in your GitHub (website) account
- `git add` — Hey git, keep track of these changes here, look at em
- `git commit` — Hey git, take a snapshot of this moment in time, so I could always go back to it
- `git reset` `--``HARD <commit hash>` — with the right commit hash, go back to that moment in time and erase any history that came after it
- `git log` — check out the history of all the commits and their messages that have been made
- `git remote add` — add a bridge (with a name, e.g. `origin`, which comes after the `remote add`, and a git link, which also comes after) to a specific place on the internet — generally, a GitHub repo (though there are other sites that work similarly to GitHub)
- `.gitignore` files for things you don’t want to save in version control but are in the directory where the git “net” (metaphorically) is


## And on GitHub…
- Milestones
- Issues
- READMEs with `.md` files
- Looking at commit history
- Linking to commits
- Forking, and figuring out what URL to clone
- Organizations to organize repositories on GitHub — act sort of in place of a user account (e.g. I have created an organization for SI507 this semester:  https://github.com/SI507-F17 , so I can create assignments for y’all to fork *in that organization* and you can fork them to your own GitHub accounts to work on them, plus the originals are all collected together in SI507-F17)



## Both together — some classic concepts for collaboration and development.

More on workflows with git, some of which will use a little bit of Git work we have not looked at yet (but which you could certainly learn and can ask us about if you want to): https://www.atlassian.com/git/tutorials/comparing-workflows

Some more nice resources to examine these ideas: https://changelog.com/posts/git-resources-for-visual-learners

This one is particularly good, I think: http://onlywei.github.io/explain-git-with-d3/#branch You can try typing git commands and see a visual representation of what’s happening beside it.


# Collaboration


## **Branching — multiple timelines**

One of the big powerful things about git.
https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell

A new branch is like a new timeline.

- `git branch branch-name` creates a new branch named **branch-name**
- `git checkout branch-name` “checks out” — makes available in the directory to edit and see — the files with the changes such as they are on the **branch-name** timeline
- Shortcut to create a new branch and check it out immediately as you create it: `git checkout -b` `**branch-name**`

Generally done as an “alternate timeline” in which to try something or build new work, with commits — that you’re not yet *sure* you want in your main, or `master`, branch, or that represents a specific thing you’re working on, or…

OR

If you’re working on a change intended for someone else’s repository, branching is one of the nice ways to make clear what’s getting done. (More on this shortly.)

The text editor **Atom** has some nice integration with GitHub, because it was built by the GitHub company. So you can do stuff like…


![](https://www.dropbox.com/s/e9b6ngnsqp7uts8/Screenshot%202017-10-24%2022.07.44.png?raw=1)


[https://www.dropbox.com/s/e9b6ngnsqp7uts8/Screenshot%202017-10-24%2022.07.44.png?dl=0](https://www.dropbox.com/s/e9b6ngnsqp7uts8/Screenshot%202017-10-24%2022.07.44.png?dl=0)

and


![](https://www.dropbox.com/s/p25rklnunnlmt17/Screenshot%202017-10-24%2022.10.31.png?raw=1)


[https://www.dropbox.com/s/p25rklnunnlmt17/Screenshot%202017-10-24%2022.10.31.png?dl=0](https://www.dropbox.com/s/p25rklnunnlmt17/Screenshot%202017-10-24%2022.10.31.png?dl=0)

Without even using the command line — but it’s useful to know how to do it on the command line; what if you don’t have access to this text editor?

What about the *old* branch(es) you had? We’ll get to that in a minute…

**Conflict timeline**

- I made a repository
- Anand forked it and made some changes on a branch
- I made some changes to my master and pushed them to GitHub
- Anand committed and pushed the branch and pull requested his changes to me
- It turns out we changed the same lines! Uh oh.
- Merge conflict.



## **Multiple remotes (not just your** `**origin**`**)**

We’ve already looked at this a little bit, but now, in more detail.

You can create a remote `origin`. But sometimes, for example, if you’ve forked a repository copy, the GitHub repository copy that is *yours* is your `origin` — the bridge to it is the `origin` bridge.

But you still want a connection to the *original* — for example, in your projects, you might still want a connection to our copy.

The convention there is to set a `remote` (a bridge, as we’ve been talking about them) to the `upstream`, and set that bridge to a URL place that corresponds to — in that case — our GitHub repository, our place on the internet.

You can set multiple `remote`s, and you can call each of them anything you want. `upstream` and `origin` are good conventions to stick by, because then others will understand your development structure.

Say you and Anand each forked the same repository of mine, and you want to be able to fetch work he did and use it with the work you’re doing. In order to be able to do that, you’ll want to set an upstream for *his* GitHub repository.

My recommendation is to use people’s names for those `remote`s, bridges to those places — or something that will help you remember what they are!

e.g. `git remote add anand-repo url-to-his-github-repository`
or
`git remote add anand url-to-his-github-repository`, etc
`git remote add another-remote-thingy url`

It’s not a good idea to set a remote that isn’t based from the same *main* repository — e.g. only things that have forked from the same source, and different people are now working on them all.

Note that we’re barely skimming the surface of the possibility of Git and GitHub collaboration here! There’s a lot to read about open source software collaboration and work, but knowing this stuff will help you understand it if you pursue that / work on OSS (Open Source Software).


## **Fetch, pull, and checkout**

A review and a reminder, now that we have more concepts to back these up.

OK, since you know how to set ‘bridges’ to a bunch of different places on the internet.

You can `git fetch` each of them. e.g. `git fetch anand-repo` or `git fetch upstream` , etc — to `fetch` basically pulls the data so you can access it on your computer — if you do the right thing next.

Options, after you fetch:

- `git checkout` (some branch of that remote, e.g. `anand/master`) — so those are the files you’re looking at
- set up a new branch of *your own* that “tracks” — among other things, starts from the end of — a branch that that remote place has — e.g. that Anand’s repo has
- `merge` a branch of that remote with a branch of your own

`git pull` is a combination of `fetch` and `merge` — all at once, pull this other thing and try to make it part of mine!

For your own space on the internet, often called `origin`, `pull` is nice and easy. Did you push something to GitHub on a computer at home, but you don’t have it on your computer at work? But the work computer has a git repo that is connected to the same online GitHub repository? Before you start working on more at work, `git pull` — it’ll fetch and merge anything that was in the remote origin.

You can also pull from not `origin` remotes — but you want to be careful in case another remote will have work that might conflict with yours.

e.g. — say you made some edits to our `README.md` to accord with what I said out loud.

We *also* updated `README.md`, but we phrased it a little bit differently, and we changed the same lines in the file. So if you want our changes…

After you edit, you try to `git pull upstream-jackie`, for example — merge conflict!

This brings us to complications of merging…

****
## `**merge**` **and resolving merge conflicts**

Another very powerful thing about git.

Git problems… pics to illustrate merge: [https://docs.google.com/document/d/1LcdVse69CKcwEgA4lrqg_Gr6YqpcqmmH81DgodR1BHU/edit](https://docs.google.com/document/d/1LcdVse69CKcwEgA4lrqg_Gr6YqpcqmmH81DgodR1BHU/edit)

`merge` → git, try to combine all changes
But git “measures” differences by lines.

What if two people make changes — and they both change the same line? How would Git know what to pick?

So, if there are changes in a line that can’t be easily *merged* with the code you’re trying to combine it with, you get a **merge conflict** to resolve.

Sometimes you might see something like this if you try to merge and there is a conflict:

![](https://lh4.googleusercontent.com/uu6chqOyGBtPxQ1OBO_gTp7kt5JiaKJ_fftdNqoBtSWA8StVXTL18gbjIAjLpRJRnrrrdK_wiPw__5AB-Qrw0OpPrugTVcsCMqQSbPwAiujzLXx6wCmg_DIJk7uhGbGwU1NkroE)


If you have a merge conflict, and you open the file (in this case, `ps8.py` ^) in your text editor, you’ll be able to find something like this:

(Note that sometimes, merge conflicts can occur even because of different *spacing* that conflicts — so you should trust that Git is right, even if it looks pretty much the same to you! Whitespace are still characters. Of course, sometimes there will be notable differences.)

(That document explains some more possible problems you may encounter when merging/variously using git.)

Demonstration of resolving a merge conflict shortly…


![](https://lh4.googleusercontent.com/E20Lkfwt_bCWbCQR6GF09no6Dl9ue08JGZjKhKHaelQ_N1x9yJ8JTpQSZ6Ei-PC8z3CeXfbHjQtWg7-r2izB66JURb8Z8d5VrYVomyznhXv0dLnOhrURYtgb0R2EGE6fDfb62LI)


Here — Orange vs Green
The first section above, called HEAD (with the GREEN), is what you most recently did, the other section is what is conflicting (with the ORANGE).

You most likely want to remove the conflicting code — but read both and decide which one should stay. (Note that ANY difference between lines in one vs the other will show up, even it’s just an extra space or tab.) YOU decide what you want.

Then commit — to resolve merge, and you can go on with whatever you were doing — like merging the conflicted code by deciding which changes you want to keep (assuming you’re the maintainer of the repo — it’s yours, or you’re one of the maintainers — and you get to decide) and continuing to work on it from that point.

# An example of using these things for a development process timeline

Link to see this on GitHub: [aerenchyma/madlib-generator#2](https://github.com/aerenchyma/madlib-generator/pull/2)

![](https://www.dropbox.com/s/5nknd9fusd3z6lq/Screenshot%202017-10-24%2021.46.49.png?raw=1)


[https://www.dropbox.com/s/5nknd9fusd3z6lq/Screenshot%202017-10-24%2021.46.49.png?dl=0](https://www.dropbox.com/s/5nknd9fusd3z6lq/Screenshot%202017-10-24%2021.46.49.png?dl=0)

![](https://www.dropbox.com/s/qx715rspw4f9srt/Screenshot%202017-10-24%2021.38.24.png?raw=1)


[https://www.dropbox.com/s/qx715rspw4f9srt/Screenshot%202017-10-24%2021.38.24.png?dl=0](https://www.dropbox.com/s/qx715rspw4f9srt/Screenshot%202017-10-24%2021.38.24.png?dl=0)

What happened here? How to fix the problem? Well —


# Project 4 Exercise I

I’ve created a repository: https://github.com/SI507-F17/nested-data-example

You should *each*:

- Fork it
- Clone it
- Create a new development branch on it. You should call the branch your **uniqname**, to make it easy for us to grade, because doing this is worth **150 points**. e.g. `cd` ‘d into the directory where your clone is, which is a git repo because it’s a clone: `git checkout -b jczetta` (my uniqname)
- Make an edit to ANY ONE OF THE LINES. Delete some of it, change it, add something to it…  whatever you want. You should still have the development branch checked out.
- Commit that change you’ve made (with the `git add` , `git commit -m` `"``message``"` process…) **to your development branch**, and push to your development branch. e.g. `git push origin jczetta` for me — my branch would be called `jczetta` b/c that’s my uniqname!
- Make a pull request to me
  - **This counts for points, making a pull request to my repo here! This is due by EOD Sunday, 11:59 PM, but you can complete it right now.** We will also send a reminder announcement about this after class.
  - When you’re done, you should link to the pull request in your Git Project - 4 assignment (along with the other 2 parts of it, so you can also do this later)

Flag one of us down if you have questions!

In a short while, we’ll get back together and I’ll demonstrate resolving the merge conflicts y’all have probably introduced if I merge your PRs.

And let’s look at a example, after…


# A bit more practice to follow along with

The power of Git version control lies partially in its ability to manipulate history asynchronously and still be collaborative and communicative

But in order to take advantage of that, you at least have to be relatively comfortable with the idea that you *can* be more comfortable with Git VCS (version control system)

There are a few typical ways to progress along a development timeline, and we’re only going to look at one, but it’s not so bad to transfer from one to another once you’ve learned a bit about manipulating Git — then you can build on that knowledge in a new team/set of collaborators to learn more about how a new group of people you’re working with generally does things.

**Personally**

- You have the main repository you’re working on
- Make a connection to a place of your own on the internet, e.g. GitHub,  and repeatedly push after you make commits, so the data about your work is backed up even if you lose access to your own computer, etc.
- You decide to try working on a new feature, e.g. …
- You create and `checkout` a new branch for development of that feature
- When the code you’re working on works and you’re sure this is something you want in your ‘main’ branch, `merge` it:
  - Make sure everything’s committed, and working, on the development branch (the new one)
  - `git checkout master` (your main timeline)
  - `git merge <dev branch name>` — merges the development branch into the master branch
  - (You can also merge master into the development one, resolve conflicts, and merge it back to master)
- Trick: there’s rarely only one way — but if you know how to manage different git commands and have an idea of what you can do, you can always sort of — get out of messes and basically maintain the history of your project
  - So you can go back to an earlier thing if you find a bug in your new branch!

**In a collaborative group**

- Fork a copy of the main repository you’re working on to your *own* internet location, which you have the rights to make edits to
- Clone it on to your own computer
- Decide what feature you are going to work on — what brief description of changes you’re going to make, e.g. …
- Create and `checkout` a new branch for that feature: a “development branch”
- Make changes, and make commits to that branch
- Try merging the branch back in to ensure that all conflicts can be resolved (though the other party could also resolve them)
- Push all your final changes to *your* branch on GitHub
- When you think it’s all set and working, make a **pull request** of that development branch to the main repository — this is done **on the GitHub online interface**
- The maintainer of the original repository can choose to accept and merge your changes
- If they do, you can then fetch from their upstream and merge back in to your own repository (this is the most step by step way, in some ways safest — first `fetch`, then `merge`)

This gets at more reasons writing good, comprehensive tests is important: when you finish the work on your development branch, you can run your test suite and make sure all the tests still pass.

Hopefully, that will be a check on whether or not you’ve broken any important functionality that already existed!

And if you’ve written tests for your new feature (Test-Driven Development), then you can see whether or not they pass to help decide whether this is something you want in a main timeline, want other people to have access to or something you want to keep working on and consider a definite part of the project.

There are also possibilities e.g. when you encounter a conflict to **force** push or pull in Git — we haven’t looked at it here, but the documentation will explain. In general the `-f` flag on a git command will do that. You want to be careful — if you force do something you don’t mean to, you *could*  still have changed something that will be hard (in a few cases, impossible) to undo. You *can* rewrite project history with Git!

Visuals…
http://onlywei.github.io/explain-git-with-d3/

# Project 4 Exercise II

With a partner! (OK to have 3 in a group, but better for most groups to have 2. May need a group of 3 to even it out; that’s OK. See instructions, below.)

Pairs: “register” yourselves here: [Canvas link]

**Instructions:**  See file here: [Canvas link]

## You’ll be…
- Practicing the above git concepts
- Moving through an abbreviated development timeline together
- Each of you assumes “a role” — so together, you’ll be doing slightly different things
- Working on this today, wrapping up together this week or in section
- Code you’re looking at is related to one of the things we’ll be looking at next
