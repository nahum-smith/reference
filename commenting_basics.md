# Creating Readable Code: Commenting
 The following includes a listing of advice and suggestions for commenting one's code.  Will be updated as more information is found.  

*"All time saved by not commenting during the coding process is made up more than twice at least by inserting comments and providing documentation after the coding process is finished."*

### Example types

**Code Commenting**  
This refers to writing descriptive variable names that are self-explanatory.  

**Inline Commenting**  
These comments come at the end of a line of code, but could also be referring to comments inside function blocks.  
Some claim this type of commenting are problematical and often useless.  This is because the very nature of an 'in-line' comments forces brevity due to the space constraints.  

**Function Comments**  
These comments are found above the function declaration and reveal necessary details about the following function. Includes: parameters, return values, and any logic nuances and/or decisions that were made.  
 
**Class / Page Commenting**  
These comments refer to an entire page or top level object.  These comments act as 'headers' and include broad overview, last edit date, associated files, author and contact information.  There is some debate about the necessity of these types of comments.  Some state that the header block organization creates unnecessary future requirements for every coder to follow the same commenting structure.  Also, to include edit dates and author information seems redundant if good version control practices are already being followed.  

### Requirement Comments

These comments act as functional indicators for a team or group of programmers during the development cycle.  They don't tell you anything specific about the code, rather they explicate what needs to be done or fixed.  This is also a great way for a solo programmer to remember bugs and things to finish/do.  Obviously, these are developmental comments that do not get pushed to production or need to be included in a finished module or block of code.  
1. TODO: This key phrase signifies what needs to be accomplished and should be placed on the  line where the future code should go.  Some environments recognize these phrase and can create to-do lists off of it.  
2. BUG / FIX: Document a specific bug, or a fix for a bug and place the comment above the line it pertains to.  If you can, include the ID of the specific BUG so you can always track where it occurred and how you fixed it.  
3. TEAMNAME: Used for larger groups or teams to indicate what sub-group worked on what portion or fixed what portion.  

### Explanatory Commenting

Items that should have explanatory comments include:
* **Startup code** - what arguments are expected and how they are handled.  How a program is initialized.  Default values and settings options for configuration variables.  
* **Exit code** - same for exit code.  return values, error codes etc. should be explained.  
* **Sub routines and functions** -  Stating the purpose with the arguments passed and returned should be explained, giving format, limits on values expected etc.  
* **long and complicated loops** -  obvious
* **Weird logic** - to enhance future maintainability of code.  This can include the switch between different coding styles: functional, OOP, Stack, sequential etc.  
* **Regular Expressions** -  regex are obscure by nature so explicating what they are aiming to catch is a good practice.


### Increasing Comment Readability
The following are some suggestions I have come across that could be used to increase readability.  

1. Commented Paragraphs - Write code/comments in paragraph format.  Break each piece of code into a sequence that achieves a single task.  
2. Precede comments by a blank line - doing this creates a distinct separation between code and comments.  
3. Properly tab comments - Make sure comments are tabbed out to the line they are referencing.  
4. Don't insult other's or your intelligence- Too many comments can be redundant and produce code smell. Don't insult the intelligence of your peers by commenting unnecessarily.  But avoid the 'programmer's hubris' as well.  There is a good proportion of comments to code that indicate a well thought out and readable system.  Find it!
5. Commenting is not Art or Design - Avoid the use of catchy characters or artsy commenting design patterns.  This will create the need for future programmers to mimic your style and they might not be pleased.  
6. Consistency - While there is much debate to how one should comment, there is little debate over whether the comments should all be consistent.  A reader should know what to expect when following your code.
7. Live Commenting - Make sure to comment while you are coding.  The chances of you commenting after you have finished are slim.  


##### Resources
1. [Successful Strategies for Commenting Your Code By Ryan Campbell](http://particletree.com/features/successful-strategies-for-commenting-code/)
2. [The Fine Art of Commenting By Bernhard Spuida](http://www.icsharpcode.net/TechNotes/Commenting20020413.pdf)
