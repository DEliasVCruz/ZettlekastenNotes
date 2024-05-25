# cli.json.jq

The standard json parser and pretty printer

## Synopsis

```sh
  jq '.' <file.json>
```

## Overview

You can use `jq` for:

- Parsing `json` files and **get values** with it's **object hierarchy based syntax**
- Displaying and **pretty printing** `json` in your terminal

## Cookbook

### Filter json based on field value

Sometimes you may have an array of json object that you want to filter and
analyze based on the value of some field included on each json object

The structure is like `jq -c '.[] | select(.<key> == <value>)' <json_file>`

For values that do not contain quotes, like numbers, then you must not include
quotes. Otherwise include the quotes for the value

```sh
  jq -c '.[] | select( ._id == 611 )' my.json

  jq -c '.[] | select( .name == "Daniel" )' my.json
```

To get the results in the form of an array you can use the `map` comand instead.
This will mutate the original array and leave only the ones that satify the
given condition

````sh

  jq -c 'map( select( ._id == 611 ) )'  my.json
````

- If your input is not a large array, but rather individual lines of json 
  then you can just use:

```sh
  jq -c 'select( ._id == 611 )' my.json
```
