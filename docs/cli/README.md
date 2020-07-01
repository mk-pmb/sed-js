
node-sed CLI
============

* __⚠__ While I try to keep the [script syntax](../script_syntax/)
  mostly compatible with [GNU sed](https://www.gnu.org/software/sed/),
  the CLI arguments are very different.
  If you need a tool with same CLI arguments as the original GNU sed,
  please use GNU sed.



Usage
-----

`node-sed command[ command[ command[ …]]]`


State
-----

To understand the command descriptions, you should know the concepts
described as the _state_ in the [script syntax docs](../script syntax/).



CLI commands
------------

* `init` –
  Reset all state to its defaults.
* `set:NAME:VALUE` –
  Set _setting_ `NAME` to `VALUE`.
* `scFile:FILENAME` –
  Add script commands from text file `FILENAME` to the CPT.
* `scArg:CODE` –
  Add script commands from literal script code `CODE` to the CPT.
* `trFile:FILENAME` –
  Read the content from text file `FILENAME` and transform it.
* `trArg:TEXT` –
  Transform the literal input text `TEXT`.




























<!-- scroll -->
