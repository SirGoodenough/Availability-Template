[![hacs_badge](https://img.shields.io/badge/HACS-Default-41BDF5.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Availability-Template)

<a href="https://www.buymeacoffee.com/SirGoodenough"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=SirGoodenough&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" width=auto, height=30/></a>
<base target="_blank">

# Availability-Template

Custom Template for checking the availability of an entity.
The main reason for using this template is not because it's complicated, it's because availability is something you will be using over and over when you are dealing with sensors, so being able to repeat the same action over and over is better if there is 1 place in your project the code exists.

# Installation

Install this in HACS or download the `availability_template.jinja` from this repository and place the files into your `config\custom_templates` directory.
[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=SirGoodenough&repository=Availability-Template&category=template)

If you cannot see templates in your HACS listing, you *may* need to enable 'experimental features' mode. To do this find the HACS section of the Home Assistant Integration page. Click on the '>' arrow to bring you to the custom integration page. Then click on configure, and select 'enable experimental features' check box. click submit, then float out and restart the HA server to make sure it takes. When you come back HACS will look slightly different, but the Templates section is now visible and you will be able to select it. At some point in time HACS will update and the new interface and options will be the only available interface.

# Availability Test

## `avail([entity1, ...])`

This expects a list of entities.

- The number of entities are counted.
- The number of entities that are NOT unknown, unavailable, empty, or none are counted.
- If the 2 counts are the same, true is returned, else false, defaults to false.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to be sure the result will render properly.

```jinja
availability: >-
    {% from 'availability_template.jinja' import avail %}
    {{- avail(['entity_1','entity_2']) | bool -}}
```

Here is a full example that uses this.  It will give you percent sunshine estimate based on data from sun angle and cloud coverage if you have those integrations in your config. (Found the state statement somewhere a while ago, sorry there is no attribution. I use it in my personal config.)

```jinja
- template
  - sensor:
    - name: "sunlight_pct"
      unique_id: 9a7586c0-0947-4b41-97e0-c0d2150bd0bb
      unit_of_measurement: "%"
      state: >-
        {%- set elevation = state_attr('sun.sun','elevation') | float %}
        {%- set cloud_coverage = states('sensor.openweathermap_cloud_coverage') | float %}
        {%- set cloud_factor = (1 - (0.75 * ( cloud_coverage / 100) ** 3 )) %}
        {%- set min_elevation = -6 %}
        {%- set max_elevation = 60 %}
        {%- set adjusted_elevation = elevation - min_elevation %}
        {%- set adjusted_elevation = [adjusted_elevation,0] | max %}
        {%- set adjusted_elevation = [adjusted_elevation,max_elevation - min_elevation] | min %}
        {%- set adjusted_elevation = adjusted_elevation / (max_elevation - min_elevation) %}
        {%- set adjusted_elevation = adjusted_elevation %}
        {%- set adjusted_elevation = adjusted_elevation * 100 %}
        {%- set brightness = adjusted_elevation * cloud_factor %}
        {{ brightness | round }}
      availability: >-
        {% from 'availability_template.jinja' import avail %}
        {{- avail(['sun.sun','sensor.openweathermap_cloud_coverage']) | bool -}}
      icon: mdi:sun-angle
      attributes:
        friendly_name: "Sunlight Percentage"

```

### Other Info

Location of this code: https://github.com/SirGoodenough/Availability-Template

Let me know if you have a suggestion.

If you have any questions, comments or additions be sure to add an issue in the above listed github repo and bring them up on my Discord Server:

### 🤹🏾‍♂️ Contact Links or see my other work

What are we Fixing Today Homepage / Website: https://www.WhatAreWeFixing.Today/

Channel Link URL: (WhatAreWeFixingToday): https://bit.ly/WhatAreWeFixingTodaysYT

What are we Fixing Today Facebook page (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodaybFB

What are we Fixing Today Twitter Account (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodayTW

Discord Guild: (Sir_Goodenough#9683): https://discord.gg/Uhmhu3B

BluePrint Library: https://github.com/SirGoodenough/HA_Blueprints/blob/master/README.md

#WhatAreWeFixingToday

#SirGoodEnough

### Disclaimer

⚠️ **DANGER OF ELECTROCUTION** ⚠️

If your device connects to mains electricity (AC power) there is danger of electrocution if not installed properly. If you don't know how to install it, please call an electrician (***Beware:*** certain countries prohibit installation without a licensed electrician present). Remember: _**SAFETY FIRST**_. It is not worth the risk to yourself, your family and your home if you don't know exactly what you are doing. Never tinker or try to flash a device using the serial programming interface while it is connected to MAINS ELECTRICITY (AC power).
