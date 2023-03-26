---
layout: post
title:  "Scoop - A command line windows installer"
date:   2023-03-25 00:00:00 +0000
categories: scoop command line windows installer
---
Recently I came across a intuitive windows command line installer caller [scoop](https://scoop.sh/){:target="_blank"}.

To install it, open a powershell terminal and run below command:

```psh
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time
> irm get.scoop.sh | iex
```

Scoop makes installing your apps a breezer. It provides an easy to search interface to search for the app you want to install. As the [site](https://scoop.sh){:target="_blank"} points out, scoop:
1. `Eliminates permission popup windows`
2. `Hides GUI wizard-style installers`
3. `Prevents PATH pollution from installing lots of programs`
4. `Avoids unexpected side-effects from installing and uninstalling programs`
5. `Finds and installs dependencies automatically`
6. `Performs all the extra setup steps itself to get a working program`

A few examples of running sample apps:

Installing NodeJS:
```psh
PS C:\> scoop install nodejs
```
`Installing 'nodejs' (18.4.0) [64bit]`

`node-v18.4.0-win-x64.7z (17.3 MB) [===================================] 100%`

`Checking hash of node-v18.4.0-win-x64.7z ... ok.`

`Extracting node-v18.4.0-win-x64.7z ... done.`

`Linking ~\scoop\apps\nodejs\current => ~\scoop\apps\nodejs\18.4.0`

`Persisting bin`

`Persisting cache`

`Running post_install script...`

`'nodejs' (18.4.0) was installed successfully!`

Installing VSCode:
```psh
PS C:\> scoop bucket add extras
```

`Checking repo... OK`

`The extras bucket was added successfully.`

```psh
PS C:\> scoop install vscode
```
`Installing 'vscode' (1.68.1) [64bit]`

`dl.7z (108.1 MB) [====================================================] 100%`

`Checking hash of dl.7z ... ok.`

`Extracting dl.7z ... done.`

`Linking ~\scoop\apps\vscode\current => ~\scoop\apps\vscode\1.68.1`

`Creating shortcut for Visual Studio Code (code.exe)`

`Persisting data`

`Running post_install script...`

`'vscode' (1.68.1) was installed successfully!`