Carbs Linux Contribution Guidelines
===================================

Thanks for taking your time to contribute! To maintain stylistic
behaviour throughout the repositories, you must adhere to these
guidelines. Exceptions may occur with good reasoning.

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Carbs Linux Contribution Guidelines](#carbs-linux-contribution-guidelines)
    - [General Conventions](#general-conventions)
    - [Shell Conventions](#shell-conventions)
    - [Plaintext Conventions (MarkDown)](#plaintext-conventions-markdown)
    - [Git Conventions](#git-conventions)

<!-- markdown-toc end -->


General Conventions
-------------------

These apply to each and every file on our repositories.

- Try to keep the file readable.
  - Characters on a line shouldn't exceed 100 characters excluding indentation.
  - Make sure you don't have code commented out during commit. Uncomment them or
    remove them.
  - Do not add comments following the code, add them to the top of the code. It
    makes it harder to read, and lines longer.

Comments should look like this.

    # Good way of commenting
    your code goes here
    
    your code goes here  # Bad way of commenting


Shell Conventions
-----------------

Shell is central to Carbs Linux projects. Most of the tools
and packages are written in POSIX sh.

- Use 4 spaces for indentation, instead of tabs.
- Make sure you don't use bash-specific code.
- Make sure you lint your code with `shellcheck` and if you
  are new to POSIX sh, use `checkbashisms`.
- Don't spawn new processes if you don't absolutely need to.
  Especially during string manipulation.
  - Never use awk. Use sed to a string if it is a complex string
    manipulation.
  - Instead of `basename $file` you should do `file=${file##*/}`.
  - Instead of `dirname  $file` you should do `file=${file%/*}` .
  - If `$file` has a suffix (`.asc`) you want to remove, instead of
    `basename $file .asc` you should do `file=${file##*/} file=${file%.asc}`.


Plaintext Conventions (MarkDown)
-------------------------------

Markdown and Plaintext conventions are the same. Even if you are
editing a Markdown file you should make it readable plaintext.
If a user downloads the repository, they should be able to read
it without the help of Github rendering it. Most repositories on
Github fail to do this, making their README file completely
unreadable when somebody decides to clone the Git repository.

**Headings**

Instead of `#` and `##` for headings use `=====` and `-----`
respectively. Using `#` is simpler, but underlines such as the
latter, give a natural sense of depth to the reader. Usage of
`###` for headers are okay as there is no replacement for them.

**Code Blocks**

Instead of ``` (three backticks) for code blocks, use 4 spaces
of indentation. Again, this gives the user a better sense of
depth when reading the file in plaintext.

**Links**

Instead of using `[link description](https://example.com/location)`,
prefer the following format.

    [link description]
    
    
    At the end of the section/file
    [link description]: https://example.com/location

**Italic and Bold Faces**

In markdown `_italics_` and `*italics*`, and `**bold**` and `__bold__`
produce the same output. However, prefer `_italics_` and `**bold**`
since they are easier to distinguish and make sense of.

Git Conventions
---------------

- You should commit a single change at a time. If you have
  multiple unrelated changes in your file, commit them seperately.
- In contrast, if you have multiple related changes across multiple
  files, commit them together.

Your commit message should be in the following format

    <file/subject>: <small commit message that will appear in shortlogs>
    
    Further long explanation that can be viewed
    in the long git logs or patches. (optional)

Here is an example commit from [kiss]

    kiss: better manifest checking
    
    This introduces a few changes in manifest checking.
    * If KISS_FORCE is specified, we don't check the manifest.
    * This will show every missing file, and won't die in the first manifest issue.
    * kiss will announce dependency checking after manifest checking is complete.

**Exceptions**

Exceptions are made for documentation, as it can be tedious to prepare
in different hunks and such. There can be punctuation and spelling
mistakes to fix. Just commit them with `file: update` where file stands
for the name of the file.

[kiss]: https://github.com/CarbsLinux/kiss
