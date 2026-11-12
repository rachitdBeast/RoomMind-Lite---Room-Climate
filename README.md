# RoomMind-Lite---Room-Climate
Thermostat-style room control inspired by RoomMind, as a plain blueprint.
Cools with a climate entity (AC), heats by switching a smart plug, and uses
an indoor temperature + humidity sensor and a weather entity for outdoor temperature.
 
 
    **Needs 3 helpers** (see roommind_lite_helpers.yaml): an input_select for the mode
    (`auto`, `heat`, `cool`, `off`, `manual`) and two input_numbers for the heat and cool target.
 
 
    **Modes:** `auto` = heat below the heat target, cool above the cool target (keep
    heat target at least 2 degrees below cool target). `heat` = heater only. `cool` = AC only.
    `off` = everything switched off. `manual` = this automation does nothing, so you can run the devices by hand.
 
 
    **Note:** in `heat` / `cool` / `off` modes the automation switches the other device off if it is running.# Markdown syntax guide

## Setup

* Paste the helpers file into your config, or create the same three helpers in the UI, then restart HA. They are a mode selector (auto, heat, cool, off, manual) and heat and cool target numbers.
* Copy `roommind_lite.yaml` to `config/blueprints/automation/roommind_lite/`.
* Go to Settings → Automations → Create → Use blueprint, and pick your entities: indoor temperature and humidity sensors, the weather entity, the AC climate entity, the heater plug, and the three helpers.
* Make one copy of the helpers and one automation for each room.

## What it does

* Heating: turns the plug on below the heat target minus the hysteresis, and off above the target plus the hysteresis.
* Cooling: the AC runs in cool mode above the cool target plus the hysteresis, and turns off below the target minus the hysteresis. It sends the AC a setpoint equal to the cool target plus an offset you can set.
* Weather entity: the outdoor temperature gates both. By default there’s no cooling below 16 °C and no heating above 22 °C, so change these for your climate.
* Humidity sensor: when the room is above 70% RH and needs no cooling or heating, the AC switches to dry mode. It stops about 5 points lower. This only applies if the AC supports dry, and you can turn it off.
* Eco: an optional schedule or presence entity switches to eco temperatures. Eco never raises the heat target or lowers the cool target.
* Protection:
  * The heater has minimum on and off times, a maximum continuous run of 180 minutes, and a hard cut-off 2 °C above target.
  * The AC has minimum on and off times to protect the compressor.
  * If the temperature sensor is unavailable or silent for 60 minutes, both devices are switched off.
