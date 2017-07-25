JSON schema dump command
========

_A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by `jq`) from a JSON document._

### List the unique paths in a JSON document

Each unique path in the JSON document is printed alongside a count of 
how many times that unique path occurs in the document.

### Count how many times each unique path occurs

For each unique path, a count of occurrences is printed to the left 
of the path.

## Synopsis

Use it like this:

    json_schema foo.json
    
If the contents of `foo.json` were the following:

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
