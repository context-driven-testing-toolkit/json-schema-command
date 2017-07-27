JSON schema dump command
========

_A wrapper for [jq](https://stedolan.github.io/jq/). Dumps the schemas
(as determined by `jq`) from a JSON document._

A `jq` wrapper that prints back a high-level view of the schema of a 
JSON document.

`json_schema` is a bash script that does two things:

1. List unique paths (using pseudocode).
1. Count how many times each unique path occurs.

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

      1 a
      1 b
      1 c
      6 c.[n]
      1 c.[n].hello
      1 d

### Sample output from NASA near-Earth objects report

This is what `json_schema` looks like when applied to a larger JSON document.

    curl -so near_earth_asteroids.json \
        https://data.nasa.gov/resource/2vr3-k9wn.json

    json_schema near_earth_asteroids.json

Then the output should look like:

    202 [n]
    202 [n].designation
    202 [n].discovery_date
    181 [n].h_mag
    202 [n].i_deg
    202 [n].moid_au
    202 [n].orbit_class
    200 [n].period_yr
    202 [n].pha
    202 [n].q_au_1
    200 [n].q_au_2

As you can see, `json_schema` presents a compact, high-level view of a
document that is composed of over 200 records.
