
<!--#echo json="package.json" key="name" underline="=" -->
sed
===
<!--/#echo -->

<!--#echo json="package.json" key="description" -->
Embrace and extend GNU sed, the stream editor for filtering and transforming
text.
<!--/#echo -->


&nbsp;

-----
-----
### Stability: Alpha preview
-----
-----



&nbsp;

API
---

This module ESM-exports an object with these methods:

### .cli(args)

Interpret the [CLI arguments](docs/cli/) given in array `args`.
Returns a promise for completion.

* __⚠__ While I try to keep the [script syntax](docs/script_syntax/)
  mostly compatible with [GNU sed](https://www.gnu.org/software/sed/),
  the CLI arguments [are very different](docs/cli/).
  If you need a tool with same CLI arguments as the original GNU sed,
  please use GNU sed.



### .transform(state[, input])

Transform text according to `state`, which should be an object with only
one property `parseTree`, whose value should be the result of `.parse`-ing
a sed script.

If `input` is…

* `null` or `undefined` (e.g. not given), return a transform stream that
  you can pipe your text into.
* a string, return a promise for the transformed stream.
* a buffer, it will be converted to a string using node's default encoding,
  then processes as if that string was given.



### .parse(script)

Parse a string `script`.
Returns a promise for an opaque truthy value that represents the parse tree.
The only purpose of exposing the parse tree is so that you can reuse it
for multiple invocations of `.transform`.

* __⚠__ "opaque" means __DO NOT rely__ on assumptions about its data format,
  as it is subject to change at any time¹, especially in patch releases.

<small>
¹ Format changes at runtime are guaranteed to be forward-compatible for
  the duration of execution. ;-)
</small>








<!--#toc stop="scan" -->



Known issues
------------

* Needs more/better tests and docs.




&nbsp;


License
-------
<!--#echo json="package.json" key=".license" -->
ISC
<!--/#echo -->
