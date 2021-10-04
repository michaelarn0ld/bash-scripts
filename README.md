# Linux Bash Scripts
----
This project serves as a means to store and share the Bash scripts and command
line tools that I use on my Linux machine. If you are interested in the Bash scripts
that I use on my MacOS machine, you can find them [here](https://gitlab.com/michaelarn0ld/bash-scripts-macos).

If you intend to use any of these scripts, it is important to ensure that they
are accessible by your ```$PATH```.


# Table of Contents
----
1. [ddg](#ddg)
1. [webcam](#webcam)
1. [zet](#zet)

|   Scripts   |   Summary                                                      |
|   :-:       |   -                                                            |
|   ddg       |   Performs a DuckDuckGo search from the terminal               |
|   webcam    |   Use a digital camera as a webcam on linux                    |
|   zet       |   Interacts with a personal [Zettelkasten](https://gitlab.com/michaelarn0ld/zettelkasten-public) |
                                                                         

## ddg
----
ddg is a command line tool that allows you to make DuckDuckGo searches right
from the terminal! Simply excecute ```ddg``` followed by what you want to
search for, and let the magic happen.

### KNOWN ISSUES
If you are using **firefox** as your default browser, if you run ```ddg```
before launching the browser, you will encounter an error when you close the
browser:
```###!!! [Parent][RunMessage] Error: Channel closing: too late to send/recv, messages will be lost```
This does not seem to affect the browsing experience and is only replicable
when you use ```ddg``` and close the browser without opening any other windows
or tabs.

### GETTING STARTED
* Determine the location of bash by running: ```which bash```

### CONFIGURATION
* Ensure the interpreter on your ```ddg``` matches the output of ```which bash```

### USAGE
```bash
ddg [ARGS...]
```


## webcam
----
Webcam is a tool for using a variety of digital cameras as webcams on Linux
systems. To see if your camera is supported, please check gPhoto2's offical
device list [here](http://gphoto.org/proj/libgphoto2/support.php).

### GETTING STARTED
There are 3 dependencies for using ```webcam```:
* gPhoto2
* v4l2loopback
* ffmpeg

To install these to your system, run:
```bash
sudo apt install gphoto2 v4l2loopback-utils ffmpeg
```

### CONFIGURATION
Load the v4l2loopback module to your kernel manually by running:
```bash
sudo modprobe v4l2loopback exclusive_caps=1 max_buffers=2
```

Keep in mind that rebooting the system will require rebooting the kernel module.
If you plan on using a digital camera as a webcam on a regular basis, it may be
worth it to ensure the module is loaded on boot by changing the modules config
file:
```bash
$ sudo vim /etc/modules

# /etc/modules: kernel modules to load at boot time.
#
# This file contains the names of kernel modules that should be loaded
# at boot time, one per line. Lines beginning with "#" are ignored.

v4l2-webcam
```

Create an alias for **v4l2-webcam**:
```bash
$ sudo vim /etc/modprobe.d/v4l2-webcam.conf

alias v4l2-webcam v4l2loopback
options v4l2loopback exclusive_caps=1 max_buffers=2
```

### USAGE
```bash
webcam [OPTION] [COMMAND]
```
|   Command                  |   Usage                                                        |
|   :-:                      |   -                                                            |
|   detect                   |   detects the camera connected to the system's USB bus         |
|   status                   |   shows a summary of the connected camera                      |
|   start                    |   starts the video stream on ```$V4L2_WEBCAM``` (see ./webcam) |
----
|   Option                   |   Usage                                                        |
|   :-:                      |   -                                                            |
|   -h, --help               |   shows usages of webcam                                       |


## zet
----
This has been inspired and influenced by [Rob Muhlestein](https://youtube.com/rwxrob).

Zet is a command line tool for creating and maintaining a personal Zettelkasten
(if you want to learn more about Zettelkasten, check mine out
[here](https://gitlab.com/michaelarn0ld/zettelkasten-public)). Please note that
this tool only works with Bash >= 4.0.

### GETTING STARTED
Before using this tool, there are a few prerequisites:
* Download ```zet``` from this repo to your machine and make sure that it is in
a place accessible by your ```$PATH``` environment variable
* In ~/.bashrc set the ```$EDITOR``` environment variable to your editor of choice
* Create a local directory where your Zettelkasten will live; make it a Git repo
and add a remote origin to your favorite Git repository hosting service.
* In this local zettelkasten directory, create a registry file ```REGISTRY.md```
* It's also a good idea to create a ```README.md``` file to describe your 
objectives for the Zettelkasten
* Determine the location of bash by running: ```which bash```

### CONFIGURATION
Now that all the prerequisites have been met, you can configure ```zet``` so
it runs on your machine. Open ```zet``` in a text editor to make changes:
* Change the interpreter on ```ddg``` to the output of ```which bash```
* Change ```PUBLIC``` to your local Zettelkasten directory
* If you want to have a private Zettelkasten, you may do the same thing for
```PRIVATE```. If you do not make a private Zettelkasten, please change this
line accordingly (note that you will not be able to use the ```-p``` or
```--private``` options).

### USAGE
```bash
zet [OPTION] [COMMAND] [ARGS...]
```
|   Command                  |   Usage                                                        |
|   :-:                      |   -                                                            |
|   all                      |   prints a list of all zettel ids in the zettelkasten          |
|   create [ZETTEL_NAME]     |   creates a new zettel                                         |
|   dir                      |   prints the session directory                                 |
|   edit [ZETTEL_ID]         |   edits an already existing zettel                             |
|   find [ZETTEL_TAG]        |   prints all zettels that have a matching tag                  |
|   isomin                   |   prints the current UTC datetime (YYYYMMDDHHMM)               |
|   link [ZETTEL_ID]         |   prints the markdown needed to link to a zettel               |
|   pull                     |   pulls the zettelkasten from its Git remote repository        |
|   push [MESSAGE]           |   pushes the local zettelkasten to its Git remote repository   |
|   read [ZETTEL_ID]         |   prints the contents of a zettel                              |
|   register [ZETTEL_TAG]    |   adds a tag to the registry if it is not there                |
|   tags [ZETTEL_ID]         |   prints all tags associated with a zettel                     |
|   topics                   |   prints all tags in the registry                              |
----
|   Option                   |   Usage                                                        |
|   :-:                      |   -                                                            |
|   -h, --help               |   shows usages of zet                                          |
|   -p, --private            |   changes default session directory from PUBLIC to PRIVATE     |


# Contributors
----
@author: Michael Arnold \
@contact: me@michaelarnold.io


# License
----
Copyright © 2021 Michael Arnold

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
