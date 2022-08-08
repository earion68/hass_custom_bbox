# hass_custom_bbox
Custom Home Assistant integration for Bbox

Based on Home Assistant Bbox integration: https://www.home-assistant.io/integrations/bbox and PyBbox: https://github.com/HydrelioxGitHub/pybbox

Merged both codes into one custom component to solve the SSL DH_KEY_TOO_SMALL issue arising from Home Assistant 2022.7 which uses an up-to-date version of OpenSSL with higher security requirements and for which Bouygues Telecom did not update the firmware.

## What has changed from the original code
A few tweaks here and there to make this work in a custom integration, but mostly the below code has been added to bboxApiCall.py:


in BboxApiCall.init method:
```python
        requests.packages.urllib3.util.ssl_.DEFAULT_CIPHERS += 'HIGH:!DH:!aNULL'
        try:
            requests.packages.urllib3.contrib.pyopenssl.DEFAULT_SSL_CIPHER_LIST += 'HIGH:!DH:!aNULL'
        except AttributeError:
            # no pyopenssl support used / needed / available
            pass
```

## Usage:
- download all files in a new folder named "custom_bbox" under "custom_components" of the Home Assistant config folder (example: /config/custom_components/custom_bbox)
- instanciate the custom component in configuration.yaml as below:

```yaml
device_tracker:
  - platform: custom_bbox
    host: 192.168.1.254
```
