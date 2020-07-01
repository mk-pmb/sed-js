
Script syntax
=============

State
-----

A lot of these concepts probably exist in GNU sed with a different name.
However, node-sed is aimed to be an alternate approach to the same problem,
rather than a reimplementation of GNU sed.

The _state_ exists even before any script command is read.
It consists of these parts:

* The _input buffer (inBuf)_ is text that has been read but not released yet.
* The _current parse tree (CPT)_
  is where node-sed remembers what to do when input is read.
  It always has an `initial node` onto which script commands can be added.
* The _global trampoline_
  is a dictionary that remembers positions in the _current parse tree_
  by custom names.
* The _command scope_ is the text that forms one command.
  It currently reaches to the end of the line.
* A _virtual command string (vCmd)_ is a sequence of zero or more characters
  that can be executed as if each of its characters were an upcoming command
  node in the CPT, with the command denoted by that character.
  Obviously this will only work for commands with a single character as
  their name.
* A _single character command (cCmd)_ is a command whose name is just one
  character. Some of them can have one or more arguments.
* The available _settings_ are:
  * `afterWork`: A vCmd to execute in case the CPT has no next command,
    usually at the end of a script.
    The supported values are `nb` (default) and `q`.
  * `autoPrint`: A vCmd to execute before each `n` or `q` command.
    The supported values are `p` (default) and the empty string.



Differences to GNU sed script syntax
------------------------------------

* At this early stage of development, the parser accepts only one
  command per line, optionally with one condition in front of it.
* Not all commands are available yet.
* Not all letter-named and numeric backslash sequences are supported.



Available cCmd
--------------

In headlines with spaces, the character before the first space is meant
literally.
The words behind the first space describe order and name of additional
syntax elements described individually.


### p

Print the inBuf.

### =

Print the number of lines read in the current transformation.

### n

Clear the inBuf and read the next line from input.
If there is no next line beause we reached the end of input, execute `q`.

### q

Stop the current transformation and abandon it.

### # comment

Ignore `comment`, which is any text remaining in the command scope.

### s sep body sep template sep flags

Apply a JavaScript RegExp string replacement on the inBuf.

* `sep` means any one of the characters `!"#$%&',/:=@|~`,
  but both `sep` have to be the same.
* `body` is the body of the JavaScript RegExp.
* `template` is the template for replacement text.
  It can contain positive single-digit backslash escape sequences
  to refer to match groups 1 to 9.
* `flags` is one or more letter to be used as flags for the
  JavaScript RegExp.
* Things that are not allowed to occurr inside `body` and `template`
  (use `\x##` or `\u####` escape sequences instead):
  * the `sep` character
  * octal character escape sequences
  * `\\` (pairs of backslashes)
  * a trailing backslash
  * `;`
  * `#`
  * `&` in template
  * `$` in template


















<!-- scroll -->
