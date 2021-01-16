#energy meter

    utility_meter:
    daily_energy:
    source: sensor.pzem_energy_kwh
    cycle: daily
    weekly_energy:
    source: sensor.pzem_energy_kwh
    cycle: weekly
    monthly_energy:
    source: sensor.pzem_energy_kwh
    cycle: monthly

#Yesterday

    - platform: template
    sensors:
      yesterday_energy:
        icon: 'mdi:counter'
        value_template: "{{ state_attr('sensor.daily_energy', 'last_period') }}

#Pricing

      energy_cost_daily:
        friendly_name: "Cost Daily"
        unit_of_measurement: '₹'
        icon_template: mdi:currency-inr
        value_template: "{{ (states('sensor.daily_energy') | float * 5.40) | round(2) }}"

      energy_cost_yesterday:
        friendly_name: "Cost Yesterday"
        unit_of_measurement: '₹'
        icon_template: mdi:currency-inr
        value_template: "{{ (states('sensor.yesterday_energy') | float * 5.40) | round(2) }}"

      energy_cost_weekly:
        friendly_name: "Cost Weekly"
        unit_of_measurement: '₹'
        icon_template: mdi:currency-inr
        value_template: "{{ (states('sensor.weekly_energy') | float * 5.40) | round(2) }}"

      energy_cost_monthly:
        friendly_name: "Cost Monthly"
        unit_of_measurement: '₹'
        icon_template: mdi:currency-inr
        value_template: "{{ (states('sensor.monthly_energy') | float * 5.40) | round(2) }}" 

#Customization        

    sensor.daily_energy:
      friendly_name: Daily energy usage
      unit_of_measurement: kWh
    sensor.yesterday_energy:
      icon: 'mdi:counter'
      friendly_name: Yesterday energy usage
      unit_of_measurement: kWh
    sensor.weekly_energy:
      friendly_name: Weekly energy usage
      unit_of_measurement: kWh
    sensor.monthly_energy:
      friendly_name: Monthly energy usage
      unit_of_measurement: kWh
