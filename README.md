# Custom filters for jinja (Home Assistant)

## Installation

*__Manual mode__*

* Place the `custom_filters` folder into your `custom_components` folder.

*__Adding custom repository to [HACS](https://hacs.xyz/)__*

* Go to the Integrations page in HACS and select the three dots in the top right corner. Select Custom repositories.
  Add repository url. Category - Integration. Read more on https://hacs.xyz/docs/faq/custom_repositories.

## Configuration

* Add `custom_filters:` to your configuration.yaml.

**Configuration Variables:**

| name                                                 | default value        | description                                                                                                                        |
| ---------------------------------------------------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **custom_date_format** <br />string (optional) | "%d %b %Y, %H:%M:%S" | Define a custom date format to use in the**format_date** filter(see [strftime cheatsheet](https://strftime.org/) for examples) |

**Example Configuration:**

```yaml
custom_filters:
    custom_date_format: "%b %-d %Y, %-I:%M:%S %p"
```

## Filters

```
replace_all                 - Replace all provided values with replacement value(s) [e.g. `replace_all("A B C D", ["B", "D"], "?")` => "`A ? C ?`"]
is_defined                  - Check if a variable is defined by it's string name [e.g. `is_defined('varname')`]
get_type                    - Return the object type (as a string) [e.g. `get_type(['A','B'])` => "`list`"]
is_type                     - Check if a value is of given type [e.g. `is_type('str', 'float')` => `true`]
inflate                     - Compress with zlib
deflate                     - Decompress with zlib
decode_base64_and_inflate   - Decode base64 content and decompress it
deflate_and_base64_encode   - Compress content and base64 encode it
decode_valetudo_map         - Decode Valetudo (https://github.com/Hypfer/Valetudo) map
urldecode                   - Decode URL characters (replace %xx escapes by their single-character equivalent)
strtolist                   - Turn a string into a list [e.g. `strtolist("['A','B','C']") | length` => `3`]
listify                     - Convert a string or non-list/dict into a list/dict (like JSON string)
get_index                   - Return the numeric index of a list or dict item [e.g. `get_index(['A','B','C'], 'A')` => `0`]
grab                        - Get a list/dict item by key, with optional fallback [e.g. `grab(['A','B','C'], 4, 'Z')` => "`Z`"]
reach                       - Get a dict item by full path of key(s), with optional fallback [e.g. `reach({"a": {"b": "c"}}, "a.b")` => "`c`"]
ternary                     - Returns one value if true, another if false, and third if null [e.g. `ternary(("a" == "b"), "Y", "N", "U")` => "`N`"]
shuffle                     - Randomize an existing list, giving a different order every invocation [e.g. `shuffle([1,2,3])` => `[2,1,3]`]
to_ascii_json               - Convert string to ASCII JSON
format_date		    - Formats a date using the "custom_date_format" defined in the configuration (see [strftime cheatsheet](https://strftime.org/) for examples). If no "custom_date_format" is provided, defaults to "%d %b %Y, %H:%M:%S" (ex: 22 Jul 2024, 18:45:12)
```

## Adding New Filters

- To add a new filter / global macro, create a function with the desired behavior and add it to the `custom_filters` array defined in `__init__.py`.
  - By default the name of the function is used as the macro/filter name
  - You can specify a custom name by adding your function as a dict with  `name` and `function` keys
