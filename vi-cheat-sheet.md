# Vi Cheat Sheet

## Modes
vi, also called VIM, has 3 modes:
- **Command**: default mode, used for navigation, copy, paste, replace, delete, quit
- **Insert**: enter this mode by typing a `i` or `a` or `o`.  Press `ESC` → return to command mode
- **Command-Line**:  press `:` or `/` or `?` while in command mode, allows user to enter commands that run after pressing **Enter**


## Movement
```
Scrolling   Mouse/trackpad can be used to scroll the text but not to place cursor for edit
h j k l     Left down up right (hold over from 1970s, just use arrow keys, Pgup, PgDn)
b w e       Word back / forward / end
0 $         Start / end of line
gg  G       First / last line
#gg #G :#   Go to line given by #, where # is a number
H M L       Go to top / middle / bottom of screen
%           Go to the matching brace, meaning: (), {}, []
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
#yy         Yank # lines, ex: 4yy copies 4 lines
p P         Paste after / before current line
```


## Delete
```
x X         Delete char at / before cursor
dw          Delete word
dd          Delete line, it is saved to buffer for later paste
D           Delete to end of line
```


## Prefix Count
User can prefix most commands with a number:
```
5dw         delete 5 words
4yy         copy 4 lines
3p          paste buffer content 3 times
```


## Search
```
/text       Search forward
?text       Search backward
n N         Next / previous match
:noh        Stop hiliting the last search
%           Go to matching brace, one of: ({[ or )}]
```


## Replace
```
:s/a/b      Replace first a with b on current line
:s/a/b/g    Replace all a on current line
:%s/a/b/g   Replace all a in file
:4,7s/a/b   On line 4 thru 7, replace only the first a
```


## Ranges
Ranges can be used with Replace and other commands.
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
:h  :help       Show VIM help - :q to quit help, note Ctrl-] and Ctrl-O, note window/tab switching below: Ctrl-w T , gt
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
This is not an exhaustive list of all RE expressions, see VIM help.  
CHAR below means character, any single letter, number, symbol.  
ATOM below means a unit of repitition, ex:  [0-9]  (ab)  .  a
```
.           Any single char except newline
*           Zero or more occurrences of prior atom, ex:  .*  a*  (ab)*  [a-z]*
+           One or more occurrences of prior atom, but you have to use \+ unless using \v mode (see below)
[b-h]       Any single character in the range b thru h, they call it a character class
\d \w \s    digit -- word -- space (incl TAB so it's whitespace)
\D \S       Not digit -- Not space
^  $        Anchor – beginning of the line -- end of line
            Note that ^ inside [] means not
[^ ]        Not space
\n          Newline
\%u         Multibyte character, eg \%u20ac -- the Euro sign €
\@=   \@!   Positive and negative lookahead -- see last example in search examples below
\@<=  \@<!  Positive and negative lookbehind -- no examples below 
```


## RE - Example Sets (aka Character classes)
```
[A-Z]       Match a single capital letter, in range A thru Z
[f-p]       Match a single lower case letter, in range f thru p
[0-9]       Match a single digit in range 0 thru 9
[abc5]      Match a single char from set [abc5]
[^abc5]     Match a single char NOT in the set [abc5]
[./=+]      Match a single char from set . / = +
[-A-F]      Match a single char that is either a dash or from range A thru F
[0-9 A-F]   Match a single char that is either a space or in range 0 thru 9 or A thru F
```


## RE - Groups (aka Capture Groups)

A group is a way to treat multiple characters as a single atom.  
Groups capture the text they match so it can be referenced later - using a back reference.  
You can have one or more groups.
```
\v          Very magic mode, it is very handy when using group syntax.  It eliminates need to use escape \ all over the place.
            After a \v all ASCII characters except 0-9, a-z, A-Z and _ have special meaning, like ( | ) + ? {}
            Using \v is like using egrep instead of grep.
\v(subpat)  Capture Group, subpat is a sub-pattern wrapped in ()
            Can contain chars and char classes, ex: ([a-f][0-9]suv) - example covered below
            Can contain | which they call alternation, ex: (40|44) - match 40 or 44
\1          Backref to contents of group 1
\2          Backref to contents of group 2 - see example below using \1 and \2
            Max of 9 groups: \1 \2 \3 ... \9
```


## RE - Search Examples
```
/Hello          Match Hello - note that regular expressions are case sensitive
/^a             Match letter a but only ones at at start of line
/.x             Match any char followed by x
/.x*            Match all text from x to the right
/34$            Match 34 only if at end of line
/^TEST          Match TEST but only at start of a line
/^TEST$         Match TEST but only if it is the only 4 chars on a line
/^[a-zA-Z]      Match first letter on a line (lower or upper case)
/^[a-z].*       Match all chars on a line that start with lower case a–z
/[D-U][c-k]     Match 2 letters, first capital D thru U, second lower case c thru k
/\v([a-f][0-9]suv)    Match 1 letter (a thru f) followed by 1 digit followed by the 3 letters suv, ex: b5suv
/\v(40|44)            Match 40 OR 44, using group syntax with very magic mode \v
/\v(\w+)-(\w+)-\1-\2  Match repeating 4 word sequence, matches both: foo-bar-foo-bar + aaa-bbb-aaa-bbb
/[0-9]          Match a single digit
/^[^#]          Match first character on a line where that char is NOT #
/fo.*nd         Match text that starts with fo and ends with nd, ex: foreground, fond
/".*"           Match double quoted text
/\v^([^"])*$    Match line with no quoted text - use very magic mode \v
/\v^(.*")@!     Result same as above but using negative lookahead @!
```
Sometimes it's just eaiser to use grep.  This will print all lines with no "
```
grep -v '"' file
```

<br>
<br>


## Not Covered Here
```
Everything RE - see the VIM help
Tags
Special keys in insert mode
Digraphs
Visual mode - v
Key mappings
Abbreviations
:set options - there are about 300+ options - for full list see VIM help
VIM startup options
Automatic Commands
Buffer list commands
Syntax highlighting options
Folding
```

<br>


# End
