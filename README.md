Assignment 1: File Explorer Application
Title
Terminal-Based File Explorer using C++

Objective
To design and implement a command-line file management tool in C++ that allows users to navigate, view, and manipulate files and directories within a Linux environment. 
The application mimics basic functionalities of the 
Linux ls, cp, mv, and rm commands while featuring both 
Normal Mode (for browsing) and Command Mode (for executing file operations).

Software Requirements
Operating System: Linux
Compiler: g++ (GNU C++ Compiler)
Library Used: <filesystem> (C++17 standard)
Build System: make

Setup Instructions:

Installation
To install g++ (if not already available):
sudo apt install g++
Compilation

In the project directory:

make
Clean Build
make clean
Execution
./main

Project Overview

The File Explorer is a terminal-based interactive program that lets users explore the file system and perform common operations directly from the command line.
It provides:

Real-time directory display
File metadata such as name, size, permissions, and timestamps
Smooth directory navigation
Dual working modes (Normal & Command)

1. Normal Mode
When the application starts, it opens in Normal Mode — a browsing interface similar to the ls -lh command output.

Features
Displays all files and directories in the current folder, including . and .. entries.

Shows attributes for each entry:
File name
File size (human-readable format)
Ownership (User and Group)
Permissions (rwx)
Last modified date
Supports vertical scrolling for directories with many entries.

Navigation:
Arrow keys for moving up and down
Enter key to:
Open a directory and view its contents
Open a file using the system’s default application

2. Command Mode

Command Mode is activated by pressing the : (colon) key.
The bottom status bar changes to accept typed commands.
Press Esc at any time to return to Normal Mode.

Supported Commands
File and Directory Operations
Copy
copy <source_file(s)> <destination_directory>

Example:
copy notes.txt report.docx ~/Documents
Move
move <source_file(s)> <destination_directory>

Example:
move sample.txt ~/Backup
Rename
rename <old_name> <new_name>

Example:
rename draft.txt final.txt
Create File / Directory
create_file <file_name> <destination_path>
create_dir <dir_name> <destination_path>


Example:
create_file notes.txt ~/Projects
create_dir new_folder ~/Projects
Delete File / Directory
delete_file <file_path>
delete_dir <directory_path>


Example:
delete_file ~/Projects/old.txt
delete_dir ~/Projects/unused_folder
Navigate to Directory
goto <directory_path>


Example:
goto /home/user/Documents
goto ~
Search for a File
search <filename>


Recursively searches the current directory and subdirectories.
Example:
search main.cpp
Snapshot the Directory Structure
snapshot <directory_path> <output_file>


Recursively lists all files and subdirectories, saving the output into the specified dump file.
Example:
snapshot ~/Projects dump.txt

3. Program Flow
Program initializes in Normal Mode, displaying the current directory’s contents.
User can:
Move around using arrow keys.
Press Enter to open files/folders.
Press : to enter Command Mode.
In Command Mode, commands are parsed and executed immediately.
Press Esc to switch back to browsing mode.

Sample Code Snippet
#include <iostream>
#include <filesystem>
#include <unistd.h>
using namespace std;
namespace fs = filesystem;

int main() {
    string currentPath = fs::current_path();
    cout << "Current Directory: " << currentPath << endl;

    for (auto &entry : fs::directory_iterator(currentPath)) {
        cout << entry.path().filename().string() << endl;
    }

    return 0;
}

Expected Output (Example Terminal View)
--------------------------------------------
| Name            Size   Owner   Permissions  Modified Date |
|------------------------------------------------------------|
| .               -      user   drwxr-xr-x   2025-11-08     |
| ..              -      user   drwxr-xr-x   2025-11-08     |
| main.cpp        2.3K   user   -rw-r--r--   2025-11-07     |
| notes.txt       1.1K   user   -rw-rw-r--   2025-11-06     |
--------------------------------------------
Status: Normal Mode | Press ':' for Command Mode

Learning Outcomes

Hands-on experience with C++ filesystem and OS interaction

Understanding terminal-based UI design and key event handling

Implementation of command parsing and process management

Practice with Makefiles and modular C++ development

Improved knowledge of Linux system programming
