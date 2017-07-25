JSON schema dump command
========

_A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by `jq`) from a JSON document._

### List the unique paths in a JSON document

Each unique path in the JSON document is printed alongside a count of 
how many times that unique path occurs in the document. Arrays of any 
length are represented with the `[]` token and array lenght is never 
considered.

### Count how many times each unique path occurs

For each unique path, a count of occurrences is printed to the left 
of the path.

## Synopsis

I have formatted the paths as valid `jq` queries, so you can feed
them back into `jq` easily.

If the input were the following JSON document:

    {
      "a": "foo",
      "b": "bar",
      "c": [1, 2, 3, {"hello": "world"}, 4, 5],
      "d": []
    }

Then that should produce output like this:

      1 .["a"]
      1 .["b"]
      1 .["c"]
      6 .["c"][]
      1 .["c"][]["hello"]
      1 .["d"]

Note that the paths listed in the output are themselves valid `jq`
queries.
