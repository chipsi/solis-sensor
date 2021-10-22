# Solis sensor integration
HomeAssistant sensor for Solis portal platform V2 (m.ginlong.com) backend. It logs in to the platform and exposes the data retrieved as sensors.
Also confirmed to work with:
* Solarman (home.solarman.ch)

> Platform V2 backend is used by Ginlong and MyEvolveCloud and the same backend is also used for different PV inverter brand portals. I've only tested it in context of Solis with the Ginlong platform. Let me know if it works with for other inverter types as well and I'll add them to the list of confirmed portals.
> :warning: This integration does not work with SolisCloud. See [Issue #18](https://github.com/hultenvp/solis-sensor/issues/18) for more details how to move to m.ginlong.com.

## HACS installation

The use of HACS is supported and is the preferred means of installing this integration.

## Manual installation

Create a directory called `solis` in the `<config directory>/custom_components/` directory on your Home Assistant instance.
Install this component by copying the files in [`/custom_components/solis/`]

"https://raw.githubusercontent.com/hultenvp/solis-sensor/master/custom_components/solis/__init__.py",
"https://raw.githubusercontent.com/hultenvp/solis-sensor/master/custom_components/solis/manifest.json"
"https://raw.githubusercontent.com/hultenvp/solis-sensor/master/custom_components/solis/const.py",
"https://raw.githubusercontent.com/hultenvp/solis-sensor/master/custom_components/solis/sensor.py",
"https://raw.githubusercontent.com/hultenvp/solis-sensor/master/custom_components/solis/platform2_portal.py"

This is how your custom_components directory should be:
```bash
custom_components
├── solis
│   ├── __init__.py
│   ├── manifest.json
│   ├── platform2_portal.py
│   ├── const.py
│   └── sensor.py
```

## Configuration example

To enable this sensor, add the following lines to your configuration.yaml file:

``` YAML
sensor:
  - platform: solis
    name: "My Solis Inverter"
    portal_domain: "m.ginlong.com"
    portal_username: "my_portal_username"
    portal_password: "my_portal_password"
    portal_plant_id: "plantId goes here"
    inverter_serial: "Serial goes here"
    sensors:
      actualpower:
      energytoday:
      status:
      temperature:
      dcinputvoltagepv1:
      dcinputcurrentpv1:
      acoutputvoltage1:
      acoutputcurrent1:
      energylastmonth:
      energythismonth:
      energythisyear:
      energytotal:
      batcapacityremaining:
      battotalenergycharged:
      battotalenergydischarged:
```

Configuration variables:

* **name** (Optional): Let you overwrite the name of the device in the frontend. *Default value: Solis*
* **portal_domain** (Optional): Portal domain name *Default value: m.ginlong.com*.
* **portal_username** (Required): Username of your portal account.
* **portal_password** (Required): Password of the portal account. 
> Note: The integration uses https to communicate with the portal, but the username and password are sent over in plain text!
* **portal_plant_id** (Required): PlantId on the platform the inverter belongs to, log into the portal to find the pland ID under tab "plants". The plantID must be a decimal value. 
> Dutch: Tab installatie: Installatie ID. 
* **inverter_serial** (Required): Serial # of the inverter itself, not the logger! Can be found under tab "devices" 
* **sensors** (Required): List of values which will be presented as sensors:
  * *actualpower*: Actual power being produced
  * *energytoday*: Total energy produced today.
  * *status*: Represents portal status. Online if portal is reachable, offline if portal is unreachable
  * *temperature*: Temperature of the inverter
  * *dcinputvoltagepv1*: String 1 DC voltage (0 if not present)
  * *dcinputvoltagepv2*: String 2 DC voltage (0 if not present)
  * *dcinputvoltagepv3*: String 3 DC voltage (0 if not present)
  * *dcinputvoltagepv4*: String 4 DC voltage (0 if not present)
  * *dcinputcurrentpv1*: String 1 DC current (0 if not present)
  * *dcinputcurrentpv2*: String 2 DC current (0 if not present)
  * *dcinputcurrentpv3*: String 3 DC current (0 if not present)
  * *dcinputcurrentpv4*: String 4 DC current (0 if not present)
  * *acoutputvoltage1* : Phase 1 AC voltage (0 if not present)
  * *acoutputvoltage2* : Phase 2 AC voltage (0 if not present)
  * *acoutputvoltage3* : Phase 3 AC voltage (0 if not present)
  * *acoutputcurrent1*: Phase 1 AC current (0 if not present)
  * *acoutputcurrent2*: Phase 2 AC current (0 if not present)
  * *acoutputcurrent3*: Phase 3 AC current (0 if not present)
  * *energylastmonth*: Total energy produced last month 
  * *energythismonth*: Total energy produced in current month
  * *energythisyear*: Total energy produced this year
  * *energytotal*: Total energy produced in the lifetime of the inverter
  * *batcapacityremaining*: Remaining battery capacity 
  * *battotalenergycharged*: Total battery energy charged
  * *battotalenergydischarged*: Total battery energy discharged


# Energy dashboard
The Solis integration now supports the energy dashboard introduced in Release 2021.8. 
> Note: This integration requires Home Assistant version 2021.9 or higher

![dashboard integration](./image/energy_dashboard_integration.GIF)
![energy production](./image/solar_production_energy_dashboard.GIF)
