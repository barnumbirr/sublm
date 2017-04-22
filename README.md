# sublm

Using git to sync your Sublime Text 3 settings across devices.

## Create the git repository

Create a .gitignore file with the following content:

```
# Ignore everything...
*
# ... except preferences
!.gitignore
!Default.sublime-mousemap
!Preferences.sublime-settings
```

If you also want to sync your packages, you can just add the following line (assuming you are using Package Control):

```
!Package Control.sublime-settings
``

This file contains a list of installed packages. If that list has changed and Sublime Text is restarted, Package Control
will automatically install missing packages, as described [here].(https://packagecontrol.io/docs/syncing)

## Set up the first device

Push your current Sublime Text settings to the remote repository.

```
$ cd /Users/<user>/Library/Application Support/Sublime Text 3/Packages/User

This is ~/AppData/Roaming/Sublime\ Text\ 3/Packages/User/ on Windows 10 and
~/.config/sublime-text-3/Packages/User on Ubuntu

$ git init
$ git remote add origin <repository url>
$ git fetch
$ git commit -am "added: settings and packages"
$ git push
```

## Set up all other devices

```
$ cd /Users/<user>/Library/Application Support/Sublime Text 3/Packages/User
$ git init
$ git remote add origin <repository url>
$ git fetch
$ git reset --hard origin/master
```

## Synchronize settings manually

```
$ git -C /Users/<user>/Library/Application Support/Sublime Text 3/Packages/User pull
``

It occurs, that the settings files differ right after pulling the current versions from the repository (especially when
Package Control loads missing packages) e.g. because of a different order of entries in the packages list or the settings
elements. In that case you can just use the hard-reset instruction to overwrite your unwanted local changes.
