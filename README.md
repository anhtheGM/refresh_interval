blueprint:
  name: LUX Refresh Interval
  description: Change the interval for the LUX inverter to refresh
  domain: automation
  input:
    luxpower_device:
      name: Dongle Serial
      description: this is the serial starting BA...
      selector:
        device:
          filter:
          - integration: luxpower
          multiple: false
    luxpower_refresh_time:
      name: Interval for the refreshing data
      description: Input the interval in seconds to refresh data.
      selector:
        select:
          options:
          - label: '20'
            value: /20
          - label: '25'
            value: /25
          - label: '30'
            value: /30
          - label: '35'
            value: /35
          - label: '40'
            value: /40
          - label: '45'
            value: /45
          - label: '50'
            value: /55
          - label: '59'
            value: /59
          custom_value: false
          multiple: false
          sort: false
  source_url: Khangminh
variables:
  luxpower_device_var: !input luxpower_device
trigger:
- platform: time_pattern
  seconds: !input luxpower_refresh_time
action:
- service: luxpower.luxpower_refresh_registers
  data:
    dongle: '{{ device_attr(luxpower_device_var, "name") }}'
    bank_count: 2
mode: single
