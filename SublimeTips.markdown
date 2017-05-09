#Sublime tips

# Cmd Palette
* ⌘⇧P 

# Navigation
* :n   Go to line n  
* ^G   Go to line shortcut
* #fz  Fuzzy search for fz
* @    Go to major section 
* ⌘R   Go to major section shortcut - also for markdown
* ⌘➡️   End of line. Hit multiple times to go to real end
* ⌥➡   Next word
* ^⌥↕  Scroll up or down
* ^⌥⇧↕ Scroll up or down by 20 lines

## History
* Move forward in history Cntrl-Shift-minus
* Move back in history Cntrl-minus

# Editing
* fn-⌫, ⇧⌫ Delete forward
* ⌘^↕  Line bubbling
* ⌘J   Join line
* ⌘⇧D  Duplicate line
* ^⇧K  Delete line
* ^↕   Change value up/down by 1
* ⌥↕   Change value up/down by 0.1
* ⌘⌥↕  Change value up/down by 10

# Selections & Cursors
* ⌘D   Select next
* ⌘K⌘D Unselect this selection and select next
* ⌘^G  Cursor to all matching
* ⌘⇧L  Convert selection to multiple cursors, 1 per line
* ⌘'   Select quoted (from SelectQuoted package)

# HTML & Wrapping (including Emmet)
* ^⇧W   Wrap with tag - gives you 2 cursors
* ⌘⇧A   Expand to enclosing tag
* ⌘K+⌘T Hide all but HTML Tag: 
* ^D    select to enclosing tag then outward
* ^J    selects inwards(from within "main") to match tags
* ^W    Wrap selected. e.g. Aijaz Ansari in .footer>b
* ⌥⇧/   Toggle comments
* ⌘'    Remove tag, usually, but that's being used by expand to quote
* ^⇧T   Go to matching tag
* ^⌥➡   Go to edit point

# Emmet Completions
* img[src="dog.jpg"][alt="Cute puppy"] → <img src="dog.jpg" alt="Cute puppy">
* Text: p{hello world} → <p>hello world</p>
* label.name[for="first"] → <label for="first"  class="name"></label>
* header+.main+footer
* header+.main>.section*3^+footer
* header+.main>.section#mySection$*3^+footer
* header+.main>.section#mySection$$*3^+footer
* header+.main>ul.menu>.a*3^+.section#mySection$$*3^+footer
* header+.main>ul.menu>.a[href="page$"]{Link$}*3^+.section#mySec3^+footer
* li.item$@5*3 # start from 5
* p.countdown$@-*10 # countdown from 10

# Coding
* ^⇧M  Select and expand to bracket
* ⌘⇧J  Python select and expand to indent

# Folding
* ⌘⌥[   Fold selected 
* ⌘⌥]   Unfold  
* ⌘K+⌘2 Fold everything at 2 or higher  
* ⌘K+⌘0 Show everything  

# Bookmarks
* ⌘F2   Create bookmark  
* F2    Cycle forward 
* ⇧F2   Cycle backwards
* ⌘⇧F2  Clear all bookmarks 
*       Select all bookmarks - gives you multiple cursors

# Origami
* ⌘K+⌘➡️  Create a pane to the ➡️ (r/l/u/d)
* ⌘K+⌘⇧➡️ Destroy pane to the r: basically, create with a shift on the direction
* ⌘K➡️    Focus to pane on rt:
* ⌘K+⇧➡  Move file to rt: Add shift ⌘KShift➡
* ⌘K⌥➡   Clone file to right

# Misc
* ⌘K+⌘U: toUpper
* ⌘K+⌘L: toLower


# Others: 
* F5   Sort file
* ⌘⇧K  Edit opening and closing tag. E.g. change a span to a div

More at: http://docs.sublimetext.info/en/latest/reference/keyboard_shortcuts_osx.html






