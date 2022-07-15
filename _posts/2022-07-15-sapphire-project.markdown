---                                                                                                                                                                         
layout: post                                                                                                                                                                
title: "Sapphire Project"                                                                                                                                                 
date: 2022-07-15 21:09:40 +0100                                                                                                                                           
tags: project github tool                                                                                                                                              
---   
## A CTF workspace organisation tool  

### Why?
I first made a (very) simple prototype of Sapphire in python to allow me to automatically set up my work area each time I played some [HackTheBox](https://hackthebox.com).  
The idea grew, and eventually I decided to create a full-fledged version of the tool in C++17, due to the speed benefits that come with it. There is still room for improvement in terms of the source code, but I hope you find Sapphire useful.  

### Features
- Use the custom shell to easily set up and manage a workspace environment for penetration testing / CTFs 
- Add up to three targets per workspace
- Make notes for each target
- view all notes taken for each target 
- visit target websites with one command
- set temporary environment variables to use when executing external commands

### Usage
Sapphire is pretty simple to install, just run `./install.sh`. To view the usage, run `./sapphire`. You can always view the usage by running 'help' within the software.

### Dependencies
[Boost](https://www.boost.org/) - for now, it is necessary to install boost prior to installing the tool. You can install it on Ubuntu/Debian with `sudo apt-get install libboost-all-dev`.  


Built and tested on Kali Linux.  

## Demo
### Usage
```
Usage: sapphire <workspace>

This will either load a workspace or create a new one..
Consider adding sapphire/ to the PATH.
To delete a workspace, simply delete its folder from the data/ directory.

Commands                                 Usage                                    Description                             
info                                                                              list all targets and their IDs, as well as workspace name
add-target                               add-target <IP>                          add a target machine to your workspace (maximum 3)
load                                     load <target-id>                         load a target to work with              
notes                                                                             display all notes made for the loaded target
make-note                                make-note <note>                         add a note for the loaded target to its note file.
back                                                                              return to the workspace directory (see !cd)
set                                      set <ENV_VAR> <value>                    set environment variables for use when using exec

Note: You may use 'set current' to set the environment variable RHOST to the IP of the currently loaded target

clear                                                                             clear the terminal                      
unload                                                                            unload the current target               
visit                                    visit <protocol> <port>                  visit the webpage of the loaded target  
help                                                                              display this help message               

Dangerous commands - these must be prefixed with a '!' to be run

cd                                       cd <dir>                                 change current working directory - MAY CAUSE ERRORS, USE CAUTIOUSLY
exec                                     exec <cmd>                               execute standard shell commands - you may wish to spawn a shell instead
                                                                                  and then 'exit' after use               
delete                                   delete <target-id>                       delete a target and everything associated with it from workspace
```

This help message can also be viewed by running 'help' in the program.

### Initialisation
[![initialisation](/assets/sapphire-project/init.png){:target="\_blank"}](/){:target="\_blank"}

Initialise or load a workspace with `sapphire <workspace-name>`. You can add a target with the `add-target` command, and list all targets with `info`. A configuration file and dedicated folder for workspace data is created for you, and can be accessed with the `exec` command (see [execution](#shell-execution)). 

### Note-taking
[![notes](/assets/sapphire-project/note.png){:target="\_blank"}](/){:target="\_blank"}

- Use `make-note` to make a note for the specific target - this can only be done if you have already selected a target
- Use `notes` to print all your notes

### Environment variable configuration
[![setenv](/assets/sapphire-project/setenv.png){:target="\_blank"}](/){:target="\_blank"}

You can set temporary environment variables during your session. They will last as long as `sapphire` is running, and are best used along with the `!exec` command (see below).

### Shell execution
[![exec](/assets/sapphire-project/exec.png){:target="\_blank"}](/){:target="\_blank"}

Execute system commands with `!exec`. To make your workflow easier, you could spawn a shell (e.g. `!exec /bin/bash`), however leaving your workspace directory may lead to unexpected behaviour.  

The directory you are working out of is named after your workspace, and contains the workspace configuration file and all your notes (in a separate notes directory). Here, you can store all data gathered from your session, and re-access it easily whenever you boot up the workspace.

### Target management
[[![tmanage](/assets/sapphire-project/delete.png){:target="\_blank"}](/){:target="\_blank"}

You can add and delete targets as you wish. If you decide to delete a target, you get a confirmation prompt, as this will delete target from the workspace configuration file, as well as all notes associated with it.

### Re-visiting a workspace
[![reopen](/assets/sapphire-project/reopen.png){:target="\_blank"}](/){:target="\_blank"}

You can open a workspace whenever you'd like. This loads up all the necessary data and places you back in the working directory.

### Visiting target sites

Although not demonstrated, using the `visit` command allows you to open the site that the target is running. To open a specific page, run `visit http(s) 80/path/to/page.html`.                                                    
