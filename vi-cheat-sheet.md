# Vi Cheat Sheet

## Modes
vi, also called vim, has 3 modes:
- **Command**: default mode, used for navigation, copy, paste, replace, delete, quit
- **Insert**: enter this mode by typing a `i` or `a` or `o`.  Press `ESC` → return to command mode
- **Command-Line**:  press `:` or `/` or `?` while in command mode, allows user to enter commands that run after pressing **Enter**



## Movement
```
h j k l     Left down up right (old school, just use arrow keys)
b w e       Word back / forward / end
0 $         Start / end of line
gg  G       First / last line
#gg #G :#   Go to line given by #, can be more than one digit
H M L       Go to top / middle / bottom of screen
%           Go to the matching (), {}, []
```


## Insert / Replace
In all cases below except one (r) user stays in this insert/replace mode until ESC key pressed.
```
i a         Insert before / after cursor
I A         Insert at start / end of line
o O         Open line below / above in insert mode
r R         Replace char at cursor with next char typed / continuously overtype chars
```


## Copy / Paste
```
yy          Yank (copy) the current line
#yy         Yank # lines, # is a number
p P         Paste after / before current line
```


## Delete
```
x X         Delete char at / before cursor
dw          Delete word
dd          Delete line
D           Delete to end of line
```


## Search
```
/text       Search forward
?text       Search backward
n N         Next / previous match
:noh        Stop hiliting the last search
```


## Replace
```
:s/a/b      Replace first a with b (line)
:s/a/b/g    Replace all on line
:%s/a/b/g   Replace all in file
```


## Prefix Count
User can prefix most commands with a number:
```
5dw         delete 5 words
4yy         copy 4 lines
3p          paste buffer content 3 times
```

## Ranges
```
:n,m         Lines n–m
:.           Current line
:$           Last line
:'c          Marker c
:%           All lines in file
:g/pattern/  All lines that contain RE pattern (see below for RE examples + the built in help guide quick ref page)
```


## Undo / Redo / Repeat
```
u  U        Undo last chg / undo all chgs to line (lower case undo can be repeated)
Ctrl-r      Redo
.           Repeat last chg
```

## Case / Join
```
~           Toggle upper/lower case for current char
#~          Toggle upper/lower case for # chars
J           Join lines (move line below to end of current line)
```

## Quit
```
:wq  ZZ     Save (write) and quit
:q   :q!    Quit / quit without saving
```

## Command-Line
Enter commands for file operations and global actions.  Note that `/` and `?` are also command-line operations.  
Press `ESC` → return to command mode  
```
:f   Ctrl-G     Show status line, filename, line#, col#, % of how far you are into the file
:44  0    $     Go to line 44 / first line / last line of file
:noh            Stop hiliting the last search
:w file         Write to file
:r file         Read file content and insert after current line
:n   :p         Next / previous file
:e file         Edit file
:e! file        Edit file, discard changes
:!cmd           Run shell command
!!cmd           Replace current line with output of cmd, ex: !!ls -al
:set nu         Show line numbers
:set nonu       Hide line numbers
:h  :help       Show help - :q to quit help, note Ctrl-] and Ctrl-O, note window/tab switching below: Ctrl-w T , gt
```

## Windows / Tabs
```
vi f1 f2 f3     Open multiple files
Ctrl-w s        Split window (also Ctrl-ws)
Ctrl-w w        Switch window (also Ctrl-ww)
Ctrl-w <arrow>  Move to window in arrow direction
:n   :N         Next / previous file
Ctrl-w T        Move window into a tab -- this is helpful if you have help open, use gt to switch tabs
:tabnew file    Open file in new tab
gt              Switch tab
:q              Quit tab or window
```

## Mark
```
m{a-zA-Z}       Mark current position with single letter mark in range {a-zA-Z}
`a              Go to mark a
``              Go to previous position
```

## Macros
```
qa              Record macro a
q               Stop recording
@a              Play macro a
```

## Regular Expressions (RE)
This is not an exhaustive list of all RE expressions, see help for all.
```
.           Any single character except newline
*           Zero or more occurrences of any character
[b-h]       Any single character in the set b thru h
[^k,p,2,4]  Any single character NOT in the set [k p 2 4]
^           Anchor – beginning of the line
$           Anchor – end of the line
\<          Anchor – beginning of word
\>          Anchor – end of word
\( .. \)    Grouping – used to group conditions - do not use, use the easier one on next line
\v( .. )    Easier VIM based grouping – same as above but eliminates need for \ all over like:  \(  \|  \)
\n          Contents of nth grouping
```

## RE - Example Sets
```
[A-Z]       Capital A to Capital Z
[a-z]       Lowercase a to lowercase z
[0-9]       Digits 0 through 9
[q,b,5,1]   Set containing q b 5 1
[./=+]      Set containing . / = +
[-A-F]      Capital A to Capital F (dash must be first)
[0-9 A-F]   Digits + space + A thru F
[D-U][c-k]  First char any capital letter D thru U, second char lower case only c thru k
```

## RE - Search Examples
```
/Hello          Match Hello - note that regular expressions are case sensitive
/^a             Match letter a but only ones at at start of line
/.x             Match any char followed by x
/.x*            Match all text from x to the right
/34$            Match only 34 at end of line
/^TEST$         Match only lines containing only TEST and not other chars
/^[a-zA-Z]      Match only the first char on a line that starts with a letter (lower or upper case)
/^[a-z].*       Match all chars on lines that start with lower case a–z
/\v(40|44)      Match lines contains 40 OR 44, using easy group syntax \v
/[0-9]          Match lines containing digits
/^[^#]          Match first character on all lines where that char is NOT #
```


<br>
<br>


## Not Covered Here
```
Tags
Special keys in insert mode
Digraphs
Visual mode - v
Key mappings
Abbreviations
:set options - there are about 300+ options - for full list see help
VIM startup options
Automatic Commands
Buffer list commands
Syntax highlighting options
Folding
```

<br>


# End
