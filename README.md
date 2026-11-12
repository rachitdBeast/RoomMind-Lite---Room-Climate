# RoomMind-Lite---Room-Climate
Thermostat-style room control inspired by RoomMind, as a plain blueprint.
Cools with a climate entity (AC), heats by switching a smart plug, and uses
an indoor temperature + humidity sensor and a weather entity for outdoor temperature.
 
 
    **Needs 3 helpers** (see roommind_lite_helpers.yaml): an input_select for the mode
    (`auto`, `heat`, `cool`, `off`, `manual`) and two input_numbers for the heat and cool target.
 
 
    **Modes:** `auto` = heat below the heat target, cool above the cool target (keep
    heat target at least 2 degrees below cool target). `heat` = heater only. `cool` = AC only.
    `off` = everything switched off. `manual` = this automation does nothing, so you can run the devices by hand.
 
 
    **Note:** in `heat` / `cool` / `off` modes the automation switches the other device off if it is running.
