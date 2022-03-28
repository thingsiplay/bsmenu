# bsmenu
bash select menu - Create menu from arguments or stdin and output selection to stdout.

A simple menu system written in Bash. A number, as well if only one entry is left, will select an entry. The selected entry is printed to stdout. Any other character is used to filter the list of available entries further down. Each argument to the program will be a menu entry. Alternatively use single dash `-` as option to read each line from stdin as a menu entry.

# Examples:

```
bsmenu Entry1 "Entry Number 2"
ls -Q | bsmenu - | xargs xdg-open 2> /dev/null
```

# Output from help:

```
$ bsmenu --help
bsmenu - bash select menu
Create menu from arguments or stdin and output selection to stdout.

CREATE

From Arguments:

  Every single argument is a list entry in the menu, unless reading from stdin.

  $ bsmenu Entry1 'Entry2' 'Entry 3'
  $ bsmenu $(ls)

From Stdin:

  If the first argument is a dash `-`, then read from stdin and list each newline seperated line as an entry in the menu. Anything after the dash will be interpreted as options to grep. grep is used when a Filter By Expression is performed.

  $ echo Entry1\n'Entry2\nEntry3' | bsmenu -
  $ ls | bsmenu - -im1

SELECT

Select By Number:

  Select an entry directly by choosing with an integer number and confirm with Enter. The value of the selected entry will be output to stdout. A '0' will just end the menu without selection.

  $ bsmenu Entry1 'Entry2' 'Entry 3'
  1) Entry1
  2) Entry2
  3) Entry 3
  #? 2
  Entry2

Filter By Expression:

  If the user input is any value other than an integer number, then that string will be interpreted as a filter to narrow down the available menu entries. All non matching entries are excluded and a new menu is generated. The Filter is an extended Regular Expression by `grep -E`. The last entry will be selected automatically.

  $ bsmenu Arch 'Fedora' 'Debian' OpenSUSE
  1) Arch
  2) Fedora
  3) Debian
  4) OpenSUSE
  #? ^.e
  
  1) Fedora
  2) Debian
  #? 1
  Fedora

Note: In case you use the hyperlink option of ls, make sure to disable it with `ls --hyperlink=never` when you use any Filter By Expression.

Copyright (c) 2022 Tuncay D.
```
