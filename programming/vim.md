Vim Tips
========
[Keith Hughitt](khughitt@umd.edu) (2012/12/12)

Just a collection of random tips and shortcuts that I have found useful while
learning Vim.

General
-------

###List Vim settings

 :set            - shows vars different from defaults
 :set all        - shows all values
 :set foo?       - shows the value of foo

 http://www.cs.swarthmore.edu/help/vim/variables.html

###Split-pane mode

 vim -o file1 file2

 <Cntl> + w <Up>/<Down> to navigate

###Buffers

    :e    <file>
    :ls   list buffers
    :b<n> switch buffers
    :bp   last buffer
    :bd   close buffer

    # buffers will not be closed but only hidden; allows switching with unsaved
    # changes.
    :set hidden

###Registers

    **Copy and paste**
    "*y  copy to primary system clipboard
    "*p  paste from primary system clipboard

    "+y  copy from selected
    "+p  paste from selected

###Modes

     http://vimdoc.sourceforge.net/htmldoc/intro.html#vim-modes-intro

    "[+]" in status-line means that changes have been made since last save.

    **Leave insert mode**
        1. <Escape>
        2. <cntl> + [
        3. <cntl> + c
        4. Alt + normal-mode key (e.g. h,j,k, or l)

###Command History

    1) "q:" or "q/" to enter command/search history
    2) Search for query of interest
    3) Edit it
    4) Enter to execute
    5) To cancel, press Cntl-c-c

    http://vim.wikia.com/wiki/Using_command-line_history

###Copy and paste

    Make sure vim is compiled with the +xterm_clipboard flag.

    1) Primary

        COPY  Select with mouse / visual mode
        PASTE Middle-mouse click

        Note: Shift + insert can also be used to paste from the primary buffer, 
        however, it takes much more effort:

            1. :set paste
            2. enter INSERT mode
            3. shift + insert

    2) Clipboard

        COPY  "+yy
        PASTE "+p

###Macros recording

    q{0-9a-zA-Z"}    start recording
    q                stop recording
    @{0-9a-zA-Z"}    repeat recording

    :help recording

###Tips

    **Cntl + o** Run one command in normal mode then return to insert mode
    **Cntl +v <Tab>** Insert normal tab with SuperTab plugin loaded

    . repeat last insert mode change

Navigation
----------

###Keyboard navigation

    **Basics**
    k up
    j down
    l right
    h left

    **Line navigation**
    0 go to beginning of line
    $ go to end of line
    ^ go to first non-whitespace character in line
    g_ go to last non-whitespace character in line

    **Word navigation**
    e go to end of current word ("end") -- letters, digits, underscores
    E go to end of current WORD -- all non white-space chars
    b go to previous word ("before")
    B go to previous word
    w go to next word
    W go to next WORD

    **Paragraph navigation**
    { go to beginning of current paragraph
    } go to end of current paragraph

    **Screen navigation**
    H go to f:irst line in screen
    M go to middle line in screen
    L go to last line in screen

    Cntl + f forward one screen
    Cntl + b backward one screen
    Cntl + d forward a half screen
    Cntl + u backward half a screen

    **file navigation**
    G   go to end of file
    gg  go to begining of file (also 1G)

    I/A insert at beginning/end of line

###Go to line <n>
    <n>G
    -or-
    :<n>

###Search

    /<text> search for "text"
    :noh    stop highlighting search results

    * search for word under cursor
    # search for word under curosr (backwords)

###Jumping

    Jump points are set for searches, substitution and marks.

    <Ctnl>o jump to previous location
    <Ctnl>i jump to newer location (same as <Tab>)
    :jumps  list jumps

    http://vim.wikia.com/wiki/Jumping_to_previously_visited_locations

Editing
-------

###Deletion

    x        Delete character
    dw       Delete word from cursor on
    daw      Delete entire word under cursor (including surrounding spaces)
    diw      Delete entire word under cursor (leave surrounding spaces)
    caw      Delete entire word under cursor and enter insert mode (c=change)
    db       Delete word backward
    dd       Delete line
    d$       Delete to end of line
    d^       Delete to beginning of line
    d<n>     d Delete n lines
    D        until end of line (same as d$)
    :21,25d  from line 21 to 25

    <ctrl>w  Delete previous word (insert mode)

###Insertion

    i before cursor
    a after cursor
    I begining of line
    A end of line
    C from current position to end of line (replaces)
    r replace one character and leave insert mode
    R ..

    <space><char> insert a character without leaving navigation mode

###Insert a string a beginning of each line
    1. Cntl + v
    2. Select lines (e.g. "475G" to select up to line 475)
    3. Shift + i
    4. type string to insert
    5. hit escape and wait ~1 second.

###Insert newline with entering insert mode

    o insert newline after current line
    O insert newline before current line

### Insert n characters

    Example, insert 80 dashes:
    * <C-o> 80 i - <Esc>
    * <Esc> 80 i - <Esc>

    http://stackoverflow.com/questions/5054128/repeating-characters-in-vim-insert-mode

Selection
---------

###Visual mode

    v cut/copy partial lines
    V cut/copy whole lines
    y yank
    d cut
    p paste

###Select multiple lines

    vnG  # select from cursor up to line n
    VnG  # select from current line up to line n
    v}   # select everything up to beginning of next paragraph

    shift + v nj   # selects next n lines

    gv  # redo previous selection

###Select using marks

    ma          # places mark a on current line
    :n          # move to line n
    Shift + v   # enter visual mode
    `a          # select back to mark a

### Switch between buffers with unsaved work


### paste mode

    # to avoid messing up indentation when pasting code, etc in
    :set paste
    (paste text...)
    :set nopaste

    # shortcut
    http://vim.wikia.com/wiki/Toggle_auto-indenting_for_code_paste

###regex find & replace

    # entire doc
    e.g. "args.var" -> "args['var']"
    %s/args\.\(\w*\)/args['\1']/

    # within visual selection
    %s/\%Vold/new/g

    # word under cursor
    *           # first start search using current workd
    %s//xyz/g   # blant
    uuuusearch uses default register (now set by above search)

###indent/unindent a block

    in visual mode:
        < unindent
        > indent

vim delete

copy text to system clipboard

    1. <Shift> + highlight text to copy
    2. middle-mouse click to paste

cut and paste multiple lines
    d<n>DOWN_ARROW
    p

cut/copy and paste (replace existing line)
    <n>G
    yy (or dd)
    <n2>G
    Vp

replace
    r - replace one character
    R - replace many characters

insert tab

    cntl + v -> Tab

    (cntl + v signals to vim that whatever character follows should be inserted
    as-is...)

    http: //stackoverflow.com/questions/6951672/how-can-i-insert-a-real-tab-character-in-vim

Useful links
------------
1. http://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim#1220118
2. http://cloudhead.io/2010/04/24/staying-the-hell-out-of-insert-mode/
3. http://vim.wikia.com/wiki/Avoid_the_escape_key
