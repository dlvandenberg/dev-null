# `jq` command
`jq` is a lightweight and flexible command-line JSON processor. Source: [jq](https://stedolan.github.io/jq/).

# Install
You can install it using _homebrew_:
```bash
$ brew install jq
```

# Usage
jq filters run on a stream of JSON data. The input is parsed as a sequence of whitespace-separated JSON values which are passed through the provided _filter_ one at a time. The output(s) of the filter are written to `stdout`,  again as a sequence of whitespace-separated JSON data.

## Basic filters
For a complete overview of basic filters, see the official [docs](https://stedolan.github.io/jq/manual/#Basicfilters).

### Identity: `.`
The identity filter, '`.`', takes it input and produces it unchanged as output. Can be used to format JSON, as _jq_ by default pretty-prints its JSON output.

#### Example
```bash
jq '.'
```

### Array/Object Value iterator: `.[]`
This filter will return all the elements of the array or all the values of the object.

## Options
The following options are possible. For a complete list, run `jq --help` or visit the [official docs](https://stedolan.github.io/jq/manual/).
- `--slurp | -s` : Read the entire input stream into a large array and run the filter just once
- `--compact-output | -c`: Do not use pretty-print but compact the output.
- `--from-file <filename> | -f <filename>`: Read filter from the file rather than from a command line.