# hass_custom_bbox
Custom Home Assistant integration for Bbox

Based on Home Assistant Bbox integration: https://www.home-assistant.io/integrations/bbox and PyBbox: https://github.com/HydrelioxGitHub/pybbox

Merged both codes into one custom component to solve:
- the SSL DH_KEY_TOO_SMALL issue arising from Home Assistant 2022.7 which uses an up-to-date version of OpenSSL with higher security requirements and for which Bouygues Telecom did not update the firmware.
- deprecated constants to be removed in 2025.1
- the Bbox firmware 23.7.8 which systematically requires login to the API

## Breaking changes
- The last version fixing the firmware 23.7.8 makes the "password" key in the configuration mandatory.
- The default host, if not mentioned, will be mabbox.bytel.fr

## Usage:
- download all files in a new folder named "custom_bbox" under "custom_components" of the Home Assistant config folder (example: /config/custom_components/custom_bbox)
- instanciate the custom component in configuration.yaml as below:

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
