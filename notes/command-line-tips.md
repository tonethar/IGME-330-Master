# Command Line Tips

## Video Link

- Video -> [Command Line Tips (11:30)](https://rit.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=e22fb8d4-2b36-4f94-9376-afc301206da3)

---

## I. Overview
- If you are going to being doing much work with ...
  - remote computers configured as *web servers*  OR 
  - running scripts (such as **Node.js** projects) on your *local* machine ...
  - then it's essential to know how to interact with the OS *shell* via a console application

---

## II. Choosing a console app
- Much of the web development being done on the command line requires the use of Unix file management commands (as opposed to Windows prompt commands). Meaning that you should use a console app that *emulates* the Unix file system commands:
  - if you are running Mac OS, it happens to be built on top of Unix, so you can simply use the built-in *Terminal* application
  - if you are running the Windows OS, you should use a console app that emulates Unix
    - [GitBash](https://gitforwindows.org/) (part of "git for Windows") is already installed on the lab machines
      - https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
    - [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal) - might be something else you could use
    - *Windows PowerShell* will usually work in a pinch
    - Using the *Windows command prompt* - **cmd.exe** - is not recommended

---

## III. Demo

- We'll be demoing the use of the most common Unix file system commands
- Below are some of the commands we'll be trying out

### III-A. Unix File Management Commands

- `cd dirName` - will change the *current working directory* to *dirName*. The current working directory is the directory we are "in" - it is where any typed in unix commands will be executed. **We will call the current working directory *cwd* below**
- `cd ..` - moves the *cwd* "up" one level into the parent directory of the folder
- `cd` - by itself, will change the *cwd* to the user's login (i.e. home) directory
- `pwd` - prints out the current path to the *cwd*
- `ls` - lists out files and directories in the *cwd*
- `ls -al` - lists out files and directories in the *cwd*, including "invisible" (those files whose name begins with a dot)
- `mkdir dirName` - will create a new folder named *dirName*
- `touch fileName` - will create an empty file named *fileName*
- `rm fileName` - will delete *fileName*
- `rmdir dirName` - will delete the folder named *dirName*
- `mv file1 file2` - will rename *file1* to *file2*
- `cp file2 file3` - will make a copy of *file2* that is named *file3*
- `chmod` - used to set file permissions
- `sudo` - used to perform commands (such as installing files in system directories) as the "super user"
- `nano` (or `pico`) - a simple text editor
- `clear` - clear the screen

**Handy Unix Command-line tips**
- *ctrl-a* - to move the cursor to the *beginning* of the line
- *ctrl-e* - to move the cursor to the *end* of the line
- *up arrow* - to view previously typed commands (continue pressing up arrow to cycle through command history, the down arrow goes forward through the history)
- *tab key* - for autocompletion of partially typed file/folder names
- *drag and drop* folders into GitBash (or Terminal) to have their file paths typed for you
- Editing what you've already typed on a line:
  - *ctrl-c* to cancel what you've typed
  - *ctrl-u* to clear up to the beginning
  - *ctrl-w* to delete a single word


**Other**
- `cat <filename>` to quickly preview the contents of a file
- `mkdir <foldername>;cd $_` to create a folder and then `cd` into it
  - `$_` is the last argument of the previous command
- more fundamental commands - https://www.math.utah.edu/lab/unix/unix-commands.html
- more fun - https://github.com/ohmyzsh/ohmyzsh/wiki
