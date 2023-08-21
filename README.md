[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Availability-Template)

# Availability-Template

Custom Template for checking the availiability of an entity.

# Installation

Install this in HACS or download the `availability_template.jinja` from this repository and place the files into your `config\custom_templates` directory.

After installation, you can edit the first line to set a default language, this will make the macros easier to use in your native language.

# Availability Test

## `avail([entity1, ...])`


This expects a list of entities.

- The number of entities are counted.
- The number of entities that are NOT unknown, unavailable, empty, or none are counted.
- If the 2 counts are the same true is returned, else false, defaults to false.


REMEMBER!!
This always returns text, so cast to bool on the other end to be certain of the result.

### Examples

```jinja
{% from 'avail.jinja' import avail %}
{%- if avail(['sensor.qotd','sensor.qotd.attributes.entries[0]']) | bool -%}
```
