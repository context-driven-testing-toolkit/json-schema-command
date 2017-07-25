JSON schema dump command
========

A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by jq) from a JSON document.

I have formatted the schemas as valid `jq` queries, so you can feed
them back into `jq` easily.

If the input were the following JSON document:

    {
      "a": "foo",
      "b": "bar",
      "c": [1, 2, 3]
    }

Then that should produce output like this:

      1 .["a"]
      1 .["b"]
      1 .["c"]
      3 .["c"][]

Note that the paths listed in the output are themselves valid `jq`
queries.
