# reading-notes


## Growth mindset is believing that your most basic abilities can be developed through dedication and hard work. This perspective creates a love of learning and a resilience that is essential for *advancement* and *great* accheivements. 

- Learning from failures
- Remembering that nothing is easy at first
- I don't know how... **yet**!

### My name is Tony Regalado. I'm a huge PC gamer, car ethusiast and animal lover. [GitHub](https://github.com/Edward-Regalado)

## These are my reading notes...

### Growth Mindset      
* Embraces Challenges   
* Persists Obstacles     
* Maximum effort      
* Learns from Criticism 

### Fixed Mindset
* Avoids Challenges 
* Loses Focus on Obstacles
* Unproductive or useless
* Ignores Criticism

### Text Editor 
* It's a piece of software that allows you to write and manage text (especially for websites)
* Can be downloaded or accessed via your web browsers
* Very important tool for web devs
* Best text editor is the one you enjoy the most- pros and cons for all of them - try them all!

### Text Editor Features
* Code completion - list possible suggestions based on what you type - saves time, less typing, less errors
* Syntax highlighting - colorizing text, easier to find errors, easier to read
* Variaty of themes- for eye strain and comfort 
* Good selection of extensions - like plugins for you text editor, adds functionality as you need it, helps you accomplish more with less effort

### OS Text Editor vs Third Party
* OS text editors work, but have less features, harder to write code, no "bells and whistles"
* Make sure you're coding in plain text - no bold, italics or underlines options
* For OS Text editor, Create folder on computer to store entire website, save files to the appropiate folder/sub-folder with correct extension (.html, .css)
* Third Party options- NotePad++, TextWrangler/BB edit, Visual Studio Code, Atom, Brackets, Sublime Text

### IDE (Integrated Development Environment)
* All-in-one package- text editor, compiler, debugger and file manager
* Similar to Microsoft Outlook - email client, calender, to-do list, task manager
* Probablly not needed for a beginner web dev

### Command line or terminal
* text based interface to the OS
* Use keyboard to type commands after prompt (user@bash)
* Command is always the first thing you type (ls), then command line arguments (-l/home/ryan)
* Use spaces between command and the first command line argument (ls -l/home/ryan)
* The first command line argument (ls) is also referred to as the option for modifying the behaviour of the command
* Options are usually listed before other arguments and typically start with a dasy (-)
* Most commands produce output texts just below the command line, some just perform their task(s) w/no display unless there was an error
* Prompt (user@bash) will be displayed again once the current command is complete - terminal is ready for anther command 

### Opening a terminal 
* Mac: Applications -> Utilities or 'command + space' (spotlight), then type Terminal 
* Linus: Applications -> System/Utilites or right-click on desktop 'Open in terminal'
* Windows: Need to SSH client like Putty 

### The Shell, Bash
* Shells are within ternimal, defines how terminal looks and behaves after running/executing commands
* Verious Shells availible- most common is Bash (Bourne again shell)
* Use command **echo** to display current shell

### Shortcuts on Linux
* commands are stored in a history, use up and down arrows to transvse history
* no need to re-type commands over and over again 
* can also edit these stored commands- use the left and right arrows to move cursor 

### Basic Navigation 
* learn basics of movingi around the system - tasks rely on being able to get to or reference the correction location
* helps work effectively in Linux  
* pwd (print working directory) tells you what your current/present directory and is **very helpful so use it often** 
* Command (ls) list what's in our current directory
* use square brackets (ls [options] [location]) means items are optional
* Most basic form (ls) single command line option
* Long listing (ls -l) displays file (-) or directory (d), owner, file size, # of blocks, modification time, group/directory of file, file name
* List directory contents (ls /etc) or (ls -l /etc) to long list current directory contents

### Paths 
* Linux files and directories on command line are called Paths
* Paths get to a particular file or directory (- or d)
* Absolute or Relatives Paths: can use either type, system will be directed to same location
* Linus file system is Hierarchical strucutre, very top is called **Root** directory (/) and has subdirectories within subdirectories
* Absolute specify a location (- or d) relative to root (/) directory, Relative specify a location (- or d) to current location and don't begin with a slash
* Shortcuts: ~(tilde) shortcut for home directory... /home/ryan/Documents or ~/Documents
* Shortcuts: .(dot) reference to Relative/current directory.. ls Documents or ./Documents 
* Shortcuts: ..(dotdot) refernce to Parent directory- used to move up the hierarchy (/home/ryan or run command ../../)
* Change Directory (cd) if you run without any arguments it will take you back to your home directory, however, (cd) usually ran with single command line
* Shortcuts: Tab Completion- hit tab key (once or multiple times) while typing command for auto complete action

### More About Files
* Linux- everything on your system is a file from text, keyboard, monitors, directories, etc. 
* Linux is an Extensionless System - file.exe (program, excutable file), file.txt (text file), file.png/gif/jpg (image file)
* Linux is case sensitive - same file name with letters of different case (file1.txt FILE1.txt File1.TXT)
* Command lines are also case sensitive - (ls verus lS) do different things
* Spaces in names - valid in files and directory names but be careful becausae it came be seen as two command lines arguments.
  For example: user@bash: ls Documents 
  file1.txt File.txt Holiday Photos 
  ...
  user@bash cd Holiday photos (incorrect) as cd moves into whichever directory is specified by the first command line argument only 
* Identify to terminal that Holiday Photos is a single command line by using '', "" or escape character \ (Holiday\ Photos)
* Shortcuts: Use Tab Completion before encountering the space, terminal will automatically escape any spaces for you
* Hidden Files and Directories- if the file or direcdtory name begins with a .(full stop) then it's considered to be hidden, can be hidden for a variety of       reasons, 
* To create a hidden file, simply rename file/directory beginning with a (.) or delete (.) to unhide
* ls -a to show hidden files and directories- user@bash ls -a Documents 
* file [path] obtain information about what type of file or directory is


### what is git? 
* is a distributed version-control system for tracking changes in source code during software dev
* A history of changes to your files 
* The ability to view, apply and remove those changes
* Keep all of your project files in one repo
* It makes collaboration possible
## Snapshots in time
* each commit has a lable that points to it
* HEAD = The label meaning "you are here"
* You can also assign a label called a message

### What is GitHub
* A way to share code
* Online place to store code
* It uses Git to help you manage your team's work
  * Version Tracking
  * Reviewing changes
  * Keep changes separate until you want to add them in 

### What is a Repository?
* Collection of file that you told Git to pay attention to
  * Usually, one project= one repo
  
