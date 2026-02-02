# Home Assistant Bbox custom

Custom Home Assistant integration for Bbox, improved for connection stability regarding [hass_custom_bbox fork](https://github.com/earion68/hass_custom_bbox). This custom component builds on the original [Home Assistant Bbox integration](https://www.home-assistant.io/integrations/bbox) and the [PyBbox library](https://github.com/HydrelioxGitHub/pybbox), merging both to address common issues and improve connectivity with Bouygues Telecom’s Bbox and adding a fix to the Bbox's login Connection stability.

## Key improvements
This version resolves:
- **Connection stability**: Reduces connectivity drops and improves the reliability of device tracking and sensor updates with Bbox.
- **SSL DH_KEY_TOO_SMALL issue**: Related to the Home Assistant 2022.7 upgrade using an updated OpenSSL version with stricter security protocols that are unsupported by Bbox firmware.
- **Deprecated constants**: Prepares the integration for changes in Home Assistant, with deprecated constants set to be removed by 2025.1.
- **API login stability**: Solves the login prompt required by Bbox firmware version 23.7.8 by enforcing a stable login process.

## Breaking changes
- Firmware 23.7.8 makes the "password" field mandatory for configuration.
- Default host, if unspecified, is set to `mabbox.bytel.fr`.

## Installation and usage:
- **Download files**: Download all files to a folder named `custom_bbox` in the `custom_components` directory of your Home Assistant config folder (e.g., `/config/custom_components/custom_bbox`).
- **Configure** in `configuration.yaml` as below:

```yaml
device_tracker:
- platform: custom_bbox
  password: YOUR_BBOX_PASSWORD_HERE # mandatory
  host: mabbox.bytel.fr # optional, some users reported it should not be added when using a different subnet (10.x.x.x)
  
sensor:
  - platform: custom_bbox
    password: YOUR_BBOX_PASSWORD_HERE # mandatory
    host: mabbox.bytel.fr  # optional, some users reported it should not be added when using a different subnet (10.x.x.x)
    monitored_variables: # pick the sensors you need below
      - down_max_bandwidth
      - up_max_bandwidth
      - current_down_bandwidth
      - current_up_bandwidth
      - uptime
      - number_of_reboots
```
