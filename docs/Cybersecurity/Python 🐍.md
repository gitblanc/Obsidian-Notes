# Use Github on Python
## Introduction

The [GitPython](https://gitpython.readthedocs.io/) project allows you to work in Python with Git repositories. In this guide we'll look at some basic operations like:

-   Initializing a repo
-   Cloning a repo
-   Adding and committing
-   Pushing and pulling with remotes
-   Checking for changes
-   Getting a diff
-   Listing and switching branches

For full documentation, see [https://gitpython.readthedocs.io/](https://gitpython.readthedocs.io/). The source code is available at [https://github.com/gitpython-developers/GitPython](https://github.com/gitpython-developers/GitPython).

## Installation

You can use `pip` to install the `gitpython` package like this:

```python
python -m pip install gitpython
```

You can also get the source code from [https://github.com/gitpython-developers/GitPython](https://github.com/gitpython-developers/GitPython) and run the `setup.py` file like this:

```python
git clone https://github.com/gitpython-developers/GitPython
cd GitPython
python setup.py install
```

## Manage repositories

Let's look at some common tasks with Git and how to do them in Python.

### Initialize a new repository

To start a new repository, you can use `git.Repo.init()` which is equivalent to running `git init`.

```python
import git

# `git init new_repo`
new_repo = git.Repo.init('new_repo')
```

This will create a new directory named `new_repo` with the `.git` directory.

### Open an existing local repo

To open an existing repo on disk, pass the repo directory ot the `Repo()` object initializer:

```python
import git

my_repo = git.Repo('existing_repo')
```

### Clone a remote repository

To clone a remote repository, use [git.Repo.clone_from()](https://gitpython.readthedocs.io/en/stable/reference.html#git.repo.base.Repo.clone_from).

```python
import git

# Check out via HTTPS
git.Repo.clone_from('https://github.com/DevDungeon/Cookbook', 'Cookbook-https')
# or clone via ssh (will use default keys)
git.Repo.clone_from('git@github.cim:DevDungeon/Cookbook', 'Cookbook-ssh')
```

### Create a clone of a local repo

You can take an existing repo, load it, and then clone that to another local repo. You might want to do this if you use the primary repository as a template for creating new projects.

```python
import git

# Load existing local repo
my_repo = git.Repo('existing_repo')
# Create a copy of the existing repo
my_repo.clone('/path/to/clone_of_existing_repo')
```

## Work with a repository

Once you have a repository, let's look at some common tasks you will perform when working with a repo like:

-   Checking if there are any changes
-   Get a diff of changes
-   Set git configuration values like user.email and user.name
-   Add and commit files
-   Manage remote repos
-   Push to remote repos
-   Creating branches
-   Listing branches
-   Switching branches

### Check if a repo has changes

To check if a repo has any changes, you can use [git.Repo.is_dirty()](https://gitpython.readthedocs.io/en/stable/reference.html#git.repo.base.Repo.is_dirty).

Here is an example that will also count untracked files as differences:

```python
import git

my_repo = git.Repo('some_repo')
if my_repo.is_dirty(untracked_files=True):
    print('Changes detected.')
```

### Get a diff of file changes

To get the differences on your current repo and see what has changed since the last commit, you can use `git.Repo.git.diff()` and pass it the tree of your last (HEAD) commit with `git.Repo.head.commit.tree`.

```python
from git import Repo

repo = Repo('my_repo')

# Check differences between current files and last commit
diff = repo.git.diff(repo.head.commit.tree)
print(diff)
```

### Configure user.name and user.mail

This next example demonstrates how to set the git config values for a repo. Here, we will set the `user.name` and `user.email` config values. The end of the example also shows how to use `config_reader()` to get configuration values.

```python
import git

repo = git.Repo.init('my_new_repo')

with repo.config_writer() as git_config:
    git_config.set_value('user', 'email', 'someone@example.com')
    git_config.set_value('user', 'name', 'John Doe')

# To check configuration values, use `config_reader()`
with repo.config_reader() as git_config:
    print(git_config.get_value('user', 'email'))
    print(git_config.get_value('user', 'name'))
```

### Add and commit files

Once you have determined that a repo has changes and what files have changed, you will want to add and then commit the files to the repository. This example will load a repo and then add two files before committing.

```python
import git

repo = git.Repo('my_repo')

# Provide a list of the files to stage
repo.index.add(['.gitignore', 'README.md'])
# Provide a commit message
repo.index.commit('Initial commit.')
```

### Work with remote repositories

If you want to push or pull from another repository, you will need to have remotes defined. This example will show you how to:

-   List remotes
-   Add remote
-   Remove remote
-   Push
-   Pull

```python
import git

repo = git.Repo('test_repo')

# List remotes
print('Remotes:')
for remote in repo.remotes:
    print(f'- {remote.name} {remote.url}')

# Create a new remote
try:
    remote = repo.create_remote('origin', url='git@github.com:NanoDano/testrepo')
except git.exc.GitCommandError as error:
    print(f'Error creating remote: {error}')

# Reference a remote by its name as part of the object
print(f'Remote name: {repo.remotes.origin.name}')
print(f'Remote URL: {repo.remotes.origin.url}')

# Delete a remote
repo.delete_remote('myremote')

# Pull from remote repo
print(repo.remotes.origin.pull())
# Push changes
print(repo.remotes.origin.push())
```

### Create and switch branches

Branching is a common task to separate development on different tasks. This example shows you how to:

-   List all branches
-   Create a new branch
-   Checkout branches

```python
import git

repo = git.Repo.init('my_new_repo')

# List all branches
for branch in repo.branches:
    print(branch)

# Create a new branch
repo.git.branch('my_new_branch')
# You need to check out the branch after creating it if you want to use it
repo.git.checkout('my_new_branch3')

# To checkout master again:
repo.git.checkout('master')
```

## Conclusion

After reading this guide you should understand how to perform common Git tasks in Python including:

-   Initializing a repo
-   Cloning a repo
-   Adding and committing
-   Pushing and pulling with remotes
-   Checking for changes
-   Listing and switching branches

---
# Create a KML file with Python

If you want a quick and dirty way to visualize datapoints on a map, python makes it easy to create a [KML file](https://developers.google.com/kml/documentation/kml_tut) that you can overlay on a map embedded on a webpage or on Google Earth.

---

Let’s say you’ve [extracted placenames](http://fredgibbs.net/extract-transform-and-save-csv-data/ "extract, transform, and save CSV data") from somwhere, and [geocoded them](http://fredgibbs.net/geocoding-a-list-of-places/ "geocoding a list of places"), and now have a file that looks like:

```text
'Charleston County, SC',32.7956561,-79.7848422
'Norfolk City, VA',36.8507689,-76.2858726
'Stafford County, VA',38.4334566,-77.4242972
'Barbour County, WV',39.1398692,-80.0087746
'York County, VA',37.2103925,-76.3868797
```

Using the python [simplekml module](http://simplekml.readthedocs.org/en/latest/index.html) makes creating a KML file of these points unfairly easy.

If you haven’t already, you’ll first need to get the [simplekml module](http://fredgibbs.net/installing-python-modules/ "installing python modules").

There are really only three crucial lines of code needed to use simplekml. 1) Create a simplekml object; 2) Add points to it; 3) Write the object to a file.

Let’s start by reading the lines of our CSV file in our usual way

```python
import csv

inputfile = csv.reader(open('geocoded-placenames.csv','r'))

for row in inputfile:
  #do something
```

Now, let’s add the necessary simplekml bits:

```python
import csv
import simplekml

inputfile = csv.reader(open('geocoded-placenames.csv','r'))
kml=simplekml.Kml()

for row in inputfile:
  kml.newpoint(name=row[0], coords=[(row[2],row[1])])

kml.save('battleplaces.kml')
```

The simplekml newpoint method requires that we send it a NAME and a COORDS, each of which we can easily pull directly from the CSV file that we’ve opened via our csv reader. Because csv.reader returns a list, we can access elements of that list by their numerical index. For the first row of our CSV file, row[0] refers to “Charleston County, SC”, and row[1] refers to 32.7956561.

We saved our coordinates as lat,long but simplekml wants them in the reverse order (long, lat), which is why we need to create the list like [(row[2],row[1])] as seen above.

So for each row in our CSV file, we create new point via the newpoint method of the kml object. Once we’ve finished with the file, we just need to call the save method on the kml object, and it will create a perfect KML file (‘battleplaces.kml’) for us.

---
# How to create a python executable file

**Step 1:**   
Install the library pyinstaller.   
Type below command in the command prompt.   
`pip install pyinstaller`

**Step 2:**   
Go into the directory where your ‘.py’ file is located.
![[Pasted image 20221107103500.png]]
**Step 3:**   
Press the shift⇧ button and simultaneously right-click at the same location. You will get the below box.
![[Pasted image 20221107103518.png]]
**Step 4:**   
Click on ‘Open PowerShell window here’.
![[Pasted image 20221107103543.png]]
You will get a window shown below.
![[Pasted image 20221107103604.png]]
**Step 5:**   
Type the command given below in that PowerShell window.   
`pyinstaller --onefile -w 'filename.py'`

Here the ‘.py’ file name is ‘1’.   
See below:
![[Pasted image 20221107103639.png]]
In case you get an error at this point in the PowerShell window like this:
![[Pasted image 20221107103705.png]]
The correction while typing the above command:   
```
.\pyinstaller --onefile -w 'filename.py'

#For any missing package:
pyinstaller --hidden-import 'package_name' --onefile 'filename.py'
```
![[Pasted image 20221107103800.png]]
**Step 6:**   
After typing the command ‘Hit the Enter’.   
It will take some time to finish the process depending on the size of the file and how big is your project.   
After the processing has been finished, the window will look as below:
![[Pasted image 20221107103818.png]]
**Step 7:**   
See the directory it should look like this:
![[Pasted image 20221107103834.png]]
‘build’ folder and ‘1.spec’ is of no use. You can delete these if you want, it will not affect your ‘.exe’ file.
![[Pasted image 20221107103858.png]]
**Step 8:**   
Open ‘dist’ folder above. Here you will get your ‘.exe’ file.
![[Pasted image 20221107103916.png]]
Right-click on the file and check the properties.
![[Pasted image 20221107103934.png]]

---
# How to use Github from python

Use the library pygithub -> https://pygithub.readthedocs.io/en/latest/index.html

---
# How to build a website in Python

Watch this video -> https://www.youtube.com/watch?v=VqgUkExPvLY

---