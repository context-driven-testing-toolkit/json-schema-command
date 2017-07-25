JSON schema dump command
========

A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by jq) from a JSON document.

I have formatted the schemas as valid `jq` queries, so you can feed
them back into `jq` easily.

If the input were the following JSON document:

    {
      "a": "apple",
      "b": "berry",
      "c": [
        "nut",
        "oat",
        "crunch"
      ]
    }

Then that should produce output like this:

      1 .["a"]
      1 .["b"]
      1 .["c"]
      3 .["c"][n]

This is a very general schema because it doesn't specify the types
(or any characteristics) of the data *in* the fields. But since I
have this list of all possible queries against my document, I can
use that list to generate a script that will drill down to each end
node in the document, producing a record of the current value of
each node.
