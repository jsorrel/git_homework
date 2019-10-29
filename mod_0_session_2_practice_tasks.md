# Session 2 Practice Tasks

The assignments listed here should take you approximately 55 total minutes.

To start this assignment, click the button in the upper right-hand corner that says **Fork**. This is now your copy of the document. Click the **Edit** button when you're ready to start adding your answers. To save your work, click the green button in the bottom right-hand corner. You can always come back and re-edit your gist.

### 1. Creating Files and Directories (10 min)

_Need help? You can go back to the files/directories portion of the lesson [here](http://mod0.turing.io/session2/#filesdirectories)._

Scroll down to the bottom of this page and look at the image of the directories and files. Use commands in your terminal to create the directories and files structured exactly how they appear in the image. 

When you're done, type `history` to see your commands. Copy and paste the commands that were used to create the directory and files:

```
  291  mkdir session_3_practice
  292  cd session_3_practice/
  293  touch budget.csv
  294  touch mentors.txt
  295  mkdir notes
  296  mkdir practice
  297  cd notes
  298  touch git_notes.txt
  299  touch command_line_notes.txt
  300  cd ../practice
  301  touch git_practice.txt
  302  mkdir projects
  303  touch projects/game.js
```

Since this is just a practice directory, feel free to remove the parent directory `session_3_practice` when you're done with this exercise. 

### 2. Git Practice (15 min)

_You can reference the files/directories portion of the lesson [here](http://mod0.turing.io/session3/#git)._

Follow the steps below to practice the git workflow. Be ready to copy-paste your terminal output as confirmation of your practice. 

1. Create a directory called `git_homework`. Inside of there, create a file called `quotes.txt`. 
1. Initialize the directory
1. Check the git status 
1. Add your `quotes.txt` file to the staging area
1. Check the git status
1. Create an initial commit
1. Check the status
1. Add your favorite quote to the `quotes.txt` file
1. Check the status
1. Check the diff
1. Add the changes to the staging area
1. Commit the new changes
1. Check the status
1. Show the log in oneline (yes, `oneline`, not a spelling error) format

Copy and paste **all** of the terminal text from this process below (not just the history):

```
jainasorrel~$ mkdir git_homework
jainasorrel~$ touch git_homework/quotes.txt
jainasorrel~$ cd git_homework/
jainasorrel~/git_homework$ git init
Initialized empty Git repository in /Users/jainasorrel/git_homework/.git/
jainasorrel~/git_homework$ git status
On branch master

No commits yet
Your favorite quote

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	quotes.txt

nothing added to commit but untracked files present (use "git add" to track)
jainasorrel~/git_homework$ git add quotes
fatal: pathspec 'quotes' did not match any files
jainasorrel~/git_homework$ git add quotes.txt
jainasorrel~/git_homework$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   quotes.txt

jainasorrel~/git_homework$ git commit -m "Initial commit"
[master (root-commit) 2d10628] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 quotes.txt
jainasorrel~/git_homework[master]$ git status
On branch master
nothing to commit, working tree clean
jainasorrel~/git_homework[master]$ vi quotes.txt
jainasorrel~/git_homework[master !]$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   quotes.txt

no changes added to commit (use "git add" and/or "git commit -a")
jainasorrel~/git_homework[master !]$ git diff
diff --git a/quotes.txt b/quotes.txt
index e69de29..b2882c9 100644
--- a/quotes.txt
+++ b/quotes.txt
@@ -0,0 +1 @@
+Your favorite quote
jainasorrel~/git_homework[master !]$ git add quotes.txt
jainasorrel~/git_homework[master !]$ git commit -m "Added Your favorite quote"
[master c86c1b3] Added Your favorite quote
 1 file changed, 1 insertion(+)
jainasorrel~/git_homework[master]$ git status
On branch master
nothing to commit, working tree clean
jainasorrel~/git_homework[master]$ git log --pretty=oneline
c86c1b3d83d4cc7866f37b771cacfd5d6754231e (HEAD -> master) Added Your favorite quote
2d10628e69dab596c6f2b210c6e461838b7bb98d Initial commit
jainasorrel~/git_homework[master]$
```

**IMPORTANT**: Do not remove this `git_homework` directory. You will be using this directory during Thursday's session. 

### 3. Classes, Attributes, and Methods (15 min)

Look at the template below for a `CardboardBox` class. Fill in missing blanks with additional attributes and methods.

Class: CardboardBox

Attributes:
- width (integer)
- depth (integer)
- height (integer)
- contents (string)

Methods:
- break_down
- stack
- store(contents)
- remove(contents)

### 4. Modify your Bash Profile (10 min)

- Make sure that you're shell is set to bash by running the following command: `$ chsh -s /bin/bash`. Remember to omit the `$`!

- [ ] Watch [this video](https://drive.google.com/file/d/1s_CDBnxHSA0HDWldjosulthAvBi-C-d5/view?usp=sharing) and follow each step to modify your own bash profile. As mentioned in the video, you will need this snippet below:

```
# get current branch in git repo
function parse_git_branch() {
  BRANCH=`git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'`
  if [ ! "${BRANCH}" == "" ]
  then
    STAT=`parse_git_dirty`
    echo "[${BRANCH}${STAT}]"
  else
    echo ""
  fi
}

# get current status of git repo
function parse_git_dirty {
  status=`git status 2>&1 | tee`
  dirty=`echo -n "${status}" 2> /dev/null | grep "modified:" &> /dev/null; echo "$?"`
  untracked=`echo -n "${status}" 2> /dev/null | grep "Untracked files" &> /dev/null; echo "$?"`
  ahead=`echo -n "${status}" 2> /dev/null | grep "Your branch is ahead of" &> /dev/null; echo "$?"`
  newfile=`echo -n "${status}" 2> /dev/null | grep "new file:" &> /dev/null; echo "$?"`
  renamed=`echo -n "${status}" 2> /dev/null | grep "renamed:" &> /dev/null; echo "$?"`
  deleted=`echo -n "${status}" 2> /dev/null | grep "deleted:" &> /dev/null; echo "$?"`
  bits=''
  if [ "${renamed}" == "0" ]; then
    bits=">${bits}"
  fi
  if [ "${ahead}" == "0" ]; then
    bits="*${bits}"
  fi
  if [ "${newfile}" == "0" ]; then
    bits="+${bits}"
  fi
  if [ "${untracked}" == "0" ]; then
    bits="?${bits}"
  fi
  if [ "${deleted}" == "0" ]; then
    bits="x${bits}"
  fi
  if [ "${dirty}" == "0" ]; then
    bits="!${bits}"
  fi
  if [ ! "${bits}" == "" ]; then
    echo " ${bits}"
  else
    echo ""
  fi
}

export PS1="\u\w\`parse_git_branch\`$ "
```

### 5. Questions/Comments/Confusions

If you have any questions, comments, or confusions that you would an instructor to address, list them below:

1. 

### Extensions

1. If time permits and you want extra git practice and alternative explanations (it's often beneficial to have something explained in many different ways), check out [Codecademy's Git Course](https://www.codecademy.com/learn/learn-git), particularly the first free item on the syllabus, "Basic Git Workflow". In Mod 0, we will not cover anything beyond Codecademy's intro section; however, you are welcome to check out the other git lessons listed on the syllabus if you want a head start. 

1. [This course](https://learnpythonthehardway.org/book/appendixa.html) is how I personally learned command line. If time permits, I highly recommend reading and practicing. 

1. Also recommended by Jeff Casimir: [Michael Hartl's Learn Enough Command Line](https://www.learnenough.com/command-line-tutorial/basics).

1. Add tab completion to make your life easier: <a href="https://gist.github.com/timomitchel/0981eeba8d69d435f94ab44f161f9bf4">Type Less. Do More.</a>
