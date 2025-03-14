---
title: Linux Commands and Terminal Commands Summary
draft: false
tags: 
aliases:
---
## Basic Shell Concepts

### What is a Shell?
- Command processor that provides interface to the kernel
- Executes commands, navigates filesystem, sets environment variables, and handles scripting

### Types of Shells
- **sh**: Original Bourne Shell
- **csh**: C Shell with improved interactive features
- **bash**: Enhanced version of sh, default in many Linux distributions
- **zsh**: Modern shell with extensive features and customization options

### Useful Shell Features
- **Auto-completion**: Press `Tab` to complete commands or filenames (double `Tab` shows options)
- **Command history**: Access previous commands with `↑` and `↓` keys
- **Command history search**: Use `Ctrl+r` to search through command history

## File System Navigation

### Directory Structure
- `/` - Root directory (top-level directory)
- Key directories:
    - `/home` - User home directories
    - `/usr` - User programs, libraries, and header files
    - `/etc` - System configuration files
    - `/var` - Variable data and logs
    - `/tmp` - Temporary files
    - `/boot` - Boot loader and kernel files
    - `/dev` - Device files
    - `/opt` - Optional/add-on software

### Path Concepts
- **Current directory**: Working directory (check with `pwd`)
- **Absolute path**: Complete path from root (starts with `/`)
    - Example: `/usr/bin/python`
- **Relative path**: Path relative to current location
    - `.` - Current directory
    - `..` - Parent directory
    - `~` - Home directory
    - Example: `../bin/python` (when in `/usr/lib`)

### Navigation Commands
- `pwd` - Print working directory
- `cd [directory]` - Change directory
    - `cd /` - Go to root directory
    - `cd ~` - Go to home directory
    - `cd ..` - Go up one directory
- `ls` - List files and directories
    - `ls -l` - Detailed listing
    - `ls -a` - Show hidden files
    - `ls -F` - Show file types with indicators
    - `ls -lh` - Human-readable file sizes

## File and Directory Operations

### File Viewing
- `cat [file]` - Display entire file content
    - `cat -n [file]` - Display with line numbers
- `head [file]` - Display first lines (default: 10)
    - `head -n 5 [file]` - Show first 5 lines
- `tail [file]` - Display last lines (default: 10)
    - `tail -n 7 [file]` - Show last 7 lines
- `less [file]` - View file with scrolling
    - Navigate: `↑`/`↓` keys, `Space` for page down, `q` to quit

### File and Directory Management
- `mkdir [directory]` - Create directory
    - `mkdir -p [path]` - Create nested directories
- `rmdir [directory]` - Remove empty directory
- `touch [file]` - Create empty file or update timestamp
- `rm [file]` - Remove file
    - `rm -r [directory]` - Remove directory and contents
    - `rm -f [file]` - Force removal without prompt
- `cp [source] [destination]` - Copy file or directory
    - `cp -r [source_dir] [destination]` - Copy directory recursively
- `mv [source] [destination]` - Move/rename file or directory

### Links
- Create hard link: `ln [target] [link_name]`
    - References same file data (inode)
    - Cannot span different filesystems or link directories
- Create symbolic link: `ln -s [target] [link_name]`
    - Like shortcuts in Windows
    - Can link to directories and across filesystems

### File Search
- `find [path] [options]` - Search for files
    - `find . -name "filename" -print` - Find by name in current directory
    - `find . -name "file*" -type f -print` - Find files starting with "file"
    - File types: `f` (file), `d` (directory), `l` (symbolic link)

## Command Help and Documentation

### Getting Help
- Basic help: `[command] --help`
- Manual pages: `man [command]`
- Info pages: `info [command]`

### Finding Commands
- `which [command]` - Show full path of command
- `whereis [command]` - Show binary, source, and manual locations
- Command search path stored in `$PATH` environment variable

## Text Editing with Vim

### Basic Vim Usage
- Open file: `vim [filename]`
- Modes:
    - Command mode (default): For navigation and commands
    - Insert mode: Enter with `i`, exit with `Esc`
- Saving and quitting:
    - `:w` - Save
    - `:q` - Quit
    - `:wq` or `:x` - Save and quit
    - `:q!` - Quit without saving

## Shell Customization

### Aliases
- Create command shortcuts
- Temporary: `alias ls='ls -F'`
- Permanent: Add to `~/.bashrc`

### Prompt Customization
- Controlled by `PS1` environment variable
    - Check current: `echo $PS1`
    - Change: `PS1='bash> '`
- Common placeholders:
    - `\u` - Username
    - `\h` - Hostname
    - `\w` - Current directory (full path)
    - `\W` - Current directory (basename only)
    - `\d` - Date
    - `\t` - Time
    - `\$` - Shows `#` for root, `$` for normal users

### Environment Variables
- View all: `printenv`
- Set variable: `export VARIABLE=value`
- Configuration files:
    - `/etc/profile` - System-wide settings
    - `~/.profile` - User-specific login settings
    - `~/.bashrc` - User-specific shell settings

## File Permissions

### Understanding Permissions
- File listing shows: `[type][user perms][group perms][others perms]`
- Permission types:
    - `r` - Read
    - `w` - Write
    - `x` - Execute
- Example: `-rw-r--r--`
    - `-` - Regular file
    - `rw-` - Owner can read and write
    - `r--` - Group can only read
    - `r--` - Others can only read

### Changing Permissions
- Symbolic mode:
    - `chmod u+w [file]` - Add write permission for user
    - `chmod g-x [file]` - Remove execute permission for group
    - `chmod o=r [file]` - Set others permission to read only
- Numeric mode:
    - `chmod 644 [file]` - Set to `-rw-r--r--`
    - `chmod 755 [file]` - Set to `-rwxr-xr-x`
    - Number calculation: read(4) + write(2) + execute(1)

### Super User Operations
- Switch to root: `su`
- Execute as root: `sudo [command]`
- Add user to sudo group: `sudo usermod -aG sudo [username]`
- Edit sudo configuration: `sudo visudo`

## Input/Output Redirection

### Redirecting Output
- `[command] > [file]` - Redirect output, overwrite file
- `[command] >> [file]` - Redirect output, append to file
- `[command] 2> [file]` - Redirect error output
- `[command] &> [file]` - Redirect both standard and error output

### Redirecting Input
- `[command] < [file]` - Use file as input source

### Pipes
- `[command1] | [command2]` - Send output of command1 as input to command2
- Example: `ls /usr/bin/gcc* | wc -l` - Count gcc files

## Package Management (APT)

### Basic APT Commands
- Update package list: `sudo apt update`
- Install package: `sudo apt install [package]`
- Remove package: `sudo apt remove [package]`
- Search for package: `apt search [keyword]`
- List installed packages: `dpkg -l`
- Show package info: `dpkg -L [package]`

## Development Tools

### Compiler Installation
- Install GCC: `sudo apt install -y gcc`
- Check installation path: `which gcc`
- List compiler files: `ls -alth $(which gcc)*`
- List toolchain tools: `ls -alth /usr/bin/$(gcc --dumpmachine)*`

### Library Management
- Install library: `sudo apt install -y libjpeg-dev`
- Check package info: `dpkg -l | grep jpeg`
- Check library location: `dpkg -L libjpeg-turbo8`
- Analyze library: `readelf -a /usr/lib/x86_64-linux-gnu/libjpeg.so.8.2.2 | grep SONAME`