# Overview

The Most Recently Used (MRU) plugin provides an easy access to a list of recently opened/edited files in Vim. This plugin automatically stores the file names as you open/edit them in Vim.

This plugin works with both Vim and Neovim and will work on all the platforms where Vim/Neovim are supported.  This plugin will work in both console and GUI Vim. This version of the MRU plugin needs Vim 7.0 and above or NeoVim..

The recently used filenames are stored in a file specified by the Vim `MRU_File` variable.

The Github repository for the MRU plugin is available at:

      https://github.com/yegappan/mru

# Installation

You can use any one of the Vim plugin managers (dein.vim, pathogen, vam, vim-plug, volt, Vundle, etc.) to install and manage this plugin.

Alternatively, you can also manually download and install the plugin using the following steps.

1. Download the mru.zip file from https://github.com/yegappan/mru/releases
1. Unzip the mru.zip file into the $HOME/.vim directory for Linux/MacOS/Unix
   systems or the $HOMEPATH/vimfiles directory for MS-Windows.  After this
   step, you should have the following files (the directory structure should
   be preserved):

	plugin/mru.vim - MRU plugin
	doc/mru.txt    - documentation (help) file

1. Start Vim and run the `:helptags ALL` command to process the help file. Without this step,
   you cannot jump to the MRU help topics.
1. Restart Vim.
1. You can use the `:MRU` command to list and edit the recently used files.
   In GUI Vim, you can use the `File->Recent Files` menu to access the
   recently used files.

To uninstall the MRU plugin, either use the uninstall command provided by the plugin manager or manually remove the plugin/mru.vim, and doc/mru.txt files from either the $HOME/.vim or $HOME/vimfiles directory.

You can also install the latest version of the plugin directly from github using the following steps (in Vim 8.0 and above): >

    $ mkdir -p $HOME/.vim/pack/downloads/start/mru
    $ cd $HOME/.vim/pack/downloads/start/mru
    $ git clone https://github.com/yegappan/mru.git

For Neovim:

    $ mkdir -p $HOME/.config/nvim/pack/downloads/start/mru
    $ cd $HOME/.config/nvim/pack/downloads/start/mru
    $ git clone https://github.com/yegappan/mru.git

# Usage
To list and edit files from the Most Recently Used (MRU) list, you can use the `:MRU` command.  The `:MRU` command displays the list of recently used files in a temporary Vim window.  If the MRU window is already opened, then the MRU list currently displayed in the window is refreshed.

Alternatively, the `:MRUToggle` command will toggle (open or close) the MRU window; so that if it is already opened, running `:MRUToggle` will close the window.

If you are using GUI Vim, then the names of the recently edited files are added to the `File->Recent Files` menu. You can select the name of a file from this sub-menu to edit the file.

You can use the normal Vim commands to move around in the MRU window. You cannot make changes in the MRU window.

In the MRU window, the following keys can be used:

Key | Description
--- | -----------
`<Enter>` | open the file under cursor
o | open the file under cursor in a horizontally split window
`<S-Enter>` | idem
O | open the file under cursor in a vertically split window
v | open the file under cursor in read-only mode
t | open the file under cursor in a tab page
p | open the file under cursor in the preview window
u | update (refresh) the MRU list
d | delete the file name under cursor from the MRU list
q | close the MRU window
`<Esc>` | idem

You can select a file name to edit by pressing the `<Enter>` key or by double clicking the left mouse button on a file name.  The selected file will be opened. If the file is already opened in a window, the cursor will be moved to that window. Otherwise, the file is opened in the previous window. If the previous window has a modified buffer or is the preview window or is used by some other plugin, then the file is opened in a new window.

You can press the `o` key to open the file name under the cursor in the MRU window in a new window. You can also press `<Shift-Enter>` instead of `o` to open the file in a new window.

To open a file from the MRU window in read-only mode (view), press the `v` key.

To open a file from the MRU window in a new tab, press the `t` key.  If the file is already opened in a window in the current or in another tab, then the cursor is moved to that tab. Otherwise, a new tab is opened.

You can open multiple files from the MRU window by specifying a count before pressing `<Enter>` or `v` or `o` or `t`. You can also visually (using linewise visual mode) select multiple filenames and invoke the commands to open the files. Each selected file will be opened in a separate window or tab.

You can press the `u` key in the MRU window to update/refresh the file list.  This is useful if you keep the MRU window open always.

You can press the `d` key to remove the entry under the cursor in the MRU window from the MRU list.

You can close the MRU window by pressing the `q` key or the `<Esc>` key or using one of the Vim window commands.

By default, the MRU window is opened as the bottom-most window. If you are using Vim version 8.0 and above, then you can use command modifiers like `:topleft` or `:botright` or `:vertical` with the :MRU command to control where the window is opened. Example:

    :topleft MRU			" horizontally split topmost window
    :botright MRU			" horizontally split bottommost window
    :vertical topleft MRU		" vertically split far-left window
    :vertical botright MRU		" vertically split far-right window

By default, the height of the MRU window is 8 or the value specified by the `g:MRU_Window_Height` variable. You can pass a count to the :MRU command to use a different height. Example:

    :15MRU
    :vertical topleft 20MRU

To display only files matching a pattern from the MRU list in the MRU window, you can specify a pattern to the `:MRU` command. Example:

    :MRU mystr

The above command displays only the file names containing the string "mystr" in them.  When you specify a partial file name and only one matching filename is found, then the `:MRU` command will edit that file.

The `:MRU` command supports command-line completion of file names from the MRU list. You can enter a partial file name and then press `<Tab>` or `<Ctrl-D>` to complete or list all the matching file names. Note that after typing the `:MRU` command, you have to enter a space before completing the file names with `<Tab>`.

When the search pattern supplied to the `:MRU` command matches only one file, then the file will be opened in the current window if it contains an
unmodified buffer. Otherwise it will be opened in a new window.  You can use command-line completion to select a file and directly open the file without opening the MRU window. If you are using Vim version 8.0 and above, you can use the command modifiers (`:leftabove`, `:rightbelow`, `:vertical`, `:tab`, etc.) to open the file in a horizontally or vertically split window or a tab page.  Example:

    :topleft MRU myfile.py		" horizontally split topmost window
    :botright MRU myfile.py		" horizontally split bottommost window
    :vertical MRU myfile.py		" vertically split window
    :vertical topleft MRU myfile.py	" vertically split far-left window
    :vertical botright MRU myfile.py	" vertically split far-right window
    :tab MRU myfile.py			" new tab page

When a file supplied to the `:MRU` command is not present in the MRU list, but it is a readable file, then the file will be opened (even though it is not present in the MRU list). This is useful if you want to open a file present in the same directory as a file in the MRU list. You can use the command-line completion of the `:MRU` command to complete the full path of a file and then modify the path to open another file present in the same path.

Whenever the MRU list changes, the MRU file is updated with the latest MRU list. When you have multiple instances of Vim running at the same time, the latest MRU list will show up in all the instances of Vim.

The `MRUFilename` syntax group is used to highlight the file names in the MRU window. By default, this syntax group is linked to the Identifier highlight group. You can change the highlight group by adding the following line in your .vimrc:

    highlight link MRUFileName LineNr

The MRU buffer uses the `mru` file type. You can use this file type to add custom auto commands, syntax highlighting, etc.

After using the MRU plugin for a period of time, the MRU list may contain files which are no longer present in the system. The `:MruRefresh` command can be used to remove non-existing files from the MRU list.

The `MruGetFiles()` function can be used to get the current list of file names in the MRU list as a `List`. This can be used with Ex commands that accept one or more file names as argument. Some example uses for this function are below:

    " search for 'my_text' in all the files in the MRU list
    :vimgrep my_text `=MruGetFiles()`

    " search for 'my_text' in the files ending in .java in the MRU list
    :vimgrep my_text `=MruGetFiles('.java')`

    " add all the .py files in the MRU list to the argument list
    :n `=MruGetFiles('.py')`

    " Add the files in MRU list to a quickfix list
    :call setqflist([], ' ', {'efm' : '%f', 'lines' : MruGetFiles()})

# Configuration

The MRU plugin supports many configurable features. These can be enabled or disabled by setting one or more variables in your .vimrc file using the `:let` command. A summary of these variables is below:

Variable Name | Description
------------- | -----------
MRU_File | name of the file containing the MRU list
MRU_Max_Entries | size of the MRU list
MRU_Exclude_Files | pattern to exclude files from MRU list
MRU_Include_Files | pattern to include files in the MRU list
MRU_Window_Height | height of the MRU window
MRU_Use_Current_Window | use current window to display MRU list
MRU_Auto_Close | close the MRU window when a file is selected
MRU_Window_Open_Always | open the MRU window even for a single file
MRU_Open_File_Use_Tabs | open files in separate tab pages
MRU_FuzzyMatch | use fuzzy match for filtering file names
MRU_Add_Menu | add MRU files to the `Recent Files` menu
MRU_Max_Menu_Entries | maximum number of entries in the MRU menu
MRU_Max_Submenu_Entries | maximum number of entries in the MRU submenu
MRU_Filename_Format | patterns to populate and parse file names in the MRU window

These variables are described in more detail below.

#### MRU_File
The list of recently edited file names is stored in the file specified by the `MRU_File` variable.  The default setting for this variable is $HOME/.vim_mru_files for Unix-like systems and $USERPROFILE/_vim_mru_files for MS-Windows systems. You can change this variable to point to a file by adding the following line to the .vimrc file:

	let MRU_File = 'd:\myhome\_vim_mru_files'

#### MRU_Max_Entries
By default, the plugin will remember the names of the last 100 used files.  As you edit more files, old file names will be removed from the MRU list.  You can set the `MRU_Max_Entries` variable to remember more file names. For example, to remember 1000 most recently used file names, you can use

	let MRU_Max_Entries = 1000

#### MRU_Exclude_Files
By default, all the edited file names are added to the MRU list. If you want to exclude file names matching a pattern, then you can set the `MRU_Exclude_Files` variable to a Vim regular expression. If any part of a file name matches the regular expression, then it is not added to the MRU list. By default, this variable is set to an empty string. For example, to not include files in the temporary (/tmp, /var/tmp and D:\temp) directories, you can set the `MRU_Exclude_Files` variable to

	let MRU_Exclude_Files = '^/tmp/.*\|^/var/tmp/.*'  " For Unix
	let MRU_Exclude_Files = '^D:\\temp\\.*'           " For MS-Windows

The specified pattern should be a Vim regular expression pattern. Note that you can specify multiple patterns using '\|'.

#### MRU_Include_Files
If you want to add only file names matching a pattern to the MRU list, then you can set the `MRU_Include_Files` variable. This variable should be set to a Vim regular expression pattern. If the regular expression matches any part of a file name, then it is added to the MRU list.  For example, to add only .c and .h files to the MRU list, you can set this variable as below:

	let MRU_Include_Files = '\.c$\|\.h$'

By default, `MRU_Include_Files` is set to an empty string and all the edited filenames are added to the MRU list. Note that you can specify multiple patterns using '\|'.

#### MRU_Window_Height
The default height of the MRU window is 8. You can set the `MRU_Window_Height` variable to change the window height. You can also set the height of the MRU window by passing a count to the :MRU command.

	let MRU_Window_Height = 15

#### MRU_Use_Current_Window
By default, when the `:MRU` command is invoked, the MRU list will be displayed in a new window. Instead, if you want the MRU plugin to reuse the current window, then you can set the `MRU_Use_Current_Window` variable to one.

	let MRU_Use_Current_Window = 1

The MRU plugin will reuse the current window. When a file name is selected, the file is also opened in the current window.

#### MRU_Auto_Close
When you select a file from the MRU window, the MRU window will be automatically closed and the selected file will be opened in the previous window. You can set the `MRU_Auto_Close` variable to zero to keep the MRU window open.

	let MRU_Auto_Close = 0

#### MRU_Window_Open_Always
When a search pattern is supplied to the :MRU command, the MRU window is opened if multiple files matching the pattern are found in the MRU list.  If only one matching file is found, instead of opening the MRU window the file is directly opened. To force open the MRU window always, you can set the `MRU_Window_Open_Always` variable to 1. By default this variable is set to 0.

	let MRU_Window_Open_Always = 1

#### MRU_Open_File_Use_Tabs
When opening a file from the MRU list, the file is opened in the current tab. If the selected file has to be opened in a tab always, then set the following variable to 1. If the file is already opened in a tab, then the cursor will be moved to that tab.

	let MRU_Open_File_Use_Tabs = 1

#### MRU_FuzzyMatch
The :MRU command accepts a string that is used to filter the file names displayed in the MRU window. The MRU command also supports command-line completion using the supplied string. If Vim supports fuzzy matching (supported from Vim 8.2.1665), then the :MRU command will fuzzy match the supplied string against the file names.  Otherwise it will use regular expression matching. To always use regular expression matching, you can set the `MRU_FuzzyMatch` variable to 0:

	let MRU_FuzzyMatch = 0

#### MRU_Add_Menu
If you don't use the `File->Recent Files` menu and want to disable it, then you can set the `MRU_Add_Menu` variable to zero. By default, the menu is enabled.

	let MRU_Add_Menu = 0

#### MRU_Max_Menu_Entries
If too many file names are present in the MRU list, then updating the MRU menu to list all the file names makes Vim slow. To avoid this, the `MRU_Max_Menu_Entries` variable controls the number of file names to show in the MRU menu. By default, this is set to 10. You can change this to show more entries in the menu.

	let MRU_Max_Menu_Entries = 20

#### MRU_Max_Submenu_Entries
If many file names are present in the MRU list, then the MRU menu is split into sub-menus. Each sub-menu contains `MRU_Max_Submenu_Entries` file names.  The default setting for this is 10. You can change this to increase the number of file names displayed in a single sub-menu:

	let MRU_Max_Submenu_Entries = 15

#### MRU_Filename_Format
In the MRU window, the filenames are displayed in two parts. The first part contains the file name without the path and the second part contains the full path to the file in parenthesis. This format is controlled by the `MRU_Filename_Format` variable. If you prefer to change this to some other format, then you can modify the `MRU_Filename_Format` variable.

The MRU_Filename_Format variable contains a `Dict` with the following keys:

Key | Description
--- | -----------
formatter | a string value containing an expression that specifies how to split/format the filename. In the expression v:val refers to the complete path to a file in the MRU list.
parser | a string value containing an regular expression that specifies how to read the filename back from a line in the MRU window.
syntax | a string value with a regular expression that matches the part to be highlighted in the MRU window.

For example, to display the full path of the files without splitting it, you can set this variable as shown below:

	let MRU_Filename_Format = {
		\ 'formatter':'v:val',
		\ 'parser':'.*',
		\ 'syntax': '[^/\\]\+$'}

# FZF Integration

You can use the MRU plugin with FZF (command-line fuzzy finder). You can download and install FZF from https://github.com/junegunn/fzf.

To select a file from the MRU file list using FZF, run the following command:

	:FZFMru

This will invoke FZF to select a file from the MRU list.
