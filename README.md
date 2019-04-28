JSON schema dump command
========

_A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by `jq`) from a JSON document._

A `jq` wrapper that prints back a high-level view of the schema of a 
JSON document.

`json_schema` is a bash script that does two things:

1. List unique paths using valid `jq` queries that you can then use 
   to retrieve those paths if you wish.
2. Count how many times each _unique_ path occurs in the document.

### List the unique paths in a JSON document

Each unique path in the JSON document is printed alongside a count of
how many times that unique path occurs in the document.

### Count how many times each unique path occurs

For each unique path, a count of occurrences is printed to the left
of the path.

The path itself is shown as a valid `jq` expression that you can then
use to access resources at paths you have identified.

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
      

### Sample output from NASA near-Earth objects report

This is what `json_schema` looks like when applied to a larger JSON document.

    curl -so near_earth_asteroids.json \
        https://data.nasa.gov/resource/2vr3-k9wn.json

    json_schema near_earth_asteroids.json

Then the output should look like:

    202 .[]
    202 .[]["designation"]
    202 .[]["discovery_date"]
    181 .[]["h_mag"]
    202 .[]["i_deg"]
    202 .[]["moid_au"]
    202 .[]["orbit_class"]
    200 .[]["period_yr"]
    202 .[]["pha"]
    202 .[]["q_au_1"]
    200 .[]["q_au_2"]

As you can see, `json_schema` presents a compact, high-level view of a
document that is composed of over 200 records. For instance, it is now
possible to see that the field `h_mag` is used much less than the other 
fields in the `near_earth_asteroids.json` document.
