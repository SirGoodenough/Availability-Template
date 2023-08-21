[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Availability-Template)

<a href="https://www.buymeacoffee.com/SirGoodenough"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=SirGoodenough&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" width=auto, height=30/></a>

# Availability-Template

Custom Template for checking the availiability of an entity.
The main reason for using this template is not because it's complicated, it's because availability is something you will be using over and over when you are dealing with sensors, so being able to repeat the same action over and over is better if there is 1 place the code exists.

# Installation

Install this in HACS or download the `availability_template.jinja` from this repository and place the files into your `config\custom_templates` directory.

After installation, you can edit the first line to set a default language, this will make the macros easier to use in your native language.

# Availability Test

## `avail([entity1, ...])`

This expects a list of entities.

- The number of entities are counted.
- The number of entities that are NOT unknown, unavailable, empty, or none are counted.
- If the 2 counts are the same, true is returned, else false, defaults to false.

REMEMBER!!
This always returns text, so cast to bool on the other end to be certain of the result.

### Examples

```jinja
{% from 'avail.jinja' import avail %}
{%- if avail(['sensor.qotd','sensor.qotd.attributes.entries[0]']) | bool -%}
```

#### Other Info

Location of this code: https://github.com/SirGoodenough/Availability-Template

Let me know if you have a suggestion.

If you have any questions, comments or additions be sure to add an issue and bring them up on my Discord Server:

#### 🤹🏾‍♂️ Contact Links or see my other work

What are we Fixing Today Homepage / Website: https://www.WhatAreWeFixing.Today/

Channel Link URL: (WhatAreWeFixingToday): https://bit.ly/WhatAreWeFixingTodaysYT

What are we Fixing Today Facebook page (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodaybFB

What are we Fixing Today Twitter Account (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodayTW

Discord Guild: (Sir_Goodenough#9683): https://discord.gg/Uhmhu3B

#WhatAreWeFixingToday

#SirGoodEnough


## Disclaimer

⚠️ **DANGER OF ELECTROCUTION** ⚠️

If your device connects to mains electricity (AC power) there is danger of electrocution if not installed properly. If you don't know how to install it, please call an electrician (***Beware:*** certain countries prohibit installation without a licensed electrician present). Remember: _**SAFETY FIRST**_. It is not worth the risk to yourself, your family and your home if you don't know exactly what you are doing. Never tinker or try to flash a device using the serial programming interface while it is connected to MAINS ELECTRICITY (AC power).
