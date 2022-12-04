# goecharger API (lite)
Lightweight Python API for accessing modern go-eCharger EV wallboxes using local HTTP API v2

[go-eCharger](https://go-e.com) models:
* Gemini
* Gemini flex
* HOMEfix
* HOME+

# Table of contents
<!-- TOC -->
* [Features](#features)
* [Installation](#installation)
* [Usage Examples](#usage-examples)
  * [Query Status](#query-status)
    * [Pretty Print Status](#pretty-print-status)
  * [Set Configuration](#set-configuration)
* [Links](#links)
<!-- TOC -->

# Features
* Query Charger Status
* Set Charger Configuration

# Installation
Directly this GitHub repository (e.g. clone).

PyPi package for `pip install` command to come ...

# Usage Examples

## Query Status
````python
from goecharger import GoeCharger

charger = GoeCharger("192.168.1.150") # --> change to your IP

# get full status
status = charger.get_status(status_type=GoeCharger.STATUS_FULL)

# only get essential status
status = charger.get_status(status_type=GoeCharger.STATUS_MINIMUM)

# get status for custom API keys (friendly name, OEM manufacturer) 
status = charger.get_status(("fna", "oem"))
````

#### Hint: Pretty Print Status
````python
import json

print(json.dumps(status, indent=4))
````
````
{
    "fna": "myEVCharger",
    "oem": "go-e"
}
````

## Set Configuration

### Generic API Key (friendly name)
````python
from goecharger import GoeCharger

charger = GoeCharger("192.168.1.150") # --> change to your IP

# set generic API key (friendly name: "myEVCharger")
charger.set_key("fna", "myEVCharger")
````

### Interrupt EV charging session
````python
from goecharger import GoeCharger

charger = GoeCharger("192.168.1.150") # --> change to your IP

# force STOP of charging session
charger.set_forced_state(charger.SettableValueEnums.ForcedState.off)

# restart charging after forced STOP
charger.set_forced_state(charger.SettableValueEnums.ForcedState.neutral)
````

# Links
[go-E Website (manufacturer)](https://go-e.com)

[go-E API v2 specification](https://github.com/goecharger/go-eCharger-API-v2/blob/main/introduction-en.md)