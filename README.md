# hass_custom_bbox
Custom Home Assistant integration for Bbox

Based on Home Assistant Bbox integration: https://www.home-assistant.io/integrations/bbox and PyBbox: https://github.com/HydrelioxGitHub/pybbox

Merged both codes into one custom component to solve the SSL issue from the new Bouygues Telecom firmware.


## Usage:
- download all files in a new folder named "custom_bbox" under "custom_components" of the Home Assistant config folder
- instanciate the custom component in configuration.yaml as below:

```yaml
device_tracker:
  - platform: custom_bbox
    host: 192.168.1.254
```
