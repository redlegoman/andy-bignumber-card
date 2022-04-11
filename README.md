# andy-bignumber-card

A simple card to display big numbers for sensors. It also supports severity levels as background. Based upon bignumber-card https://github.com/custom-cards/bignumber-card.git


**Options**

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:bignumber-card`
| title | string | optional | Name to display on card
| scale | string | 50px | Base scale for card: '50px'
| entity | string | **Required** | `sensor.my_temperature`
| attribute | string | optional | the entity attribute you want to display e.g. `current_temperature`.  The entity state will be shown if not defined.
| min | number | optional | Minimum value. If specified you get bar display
| max | number | optional | Maximum value. Must be specified if you added min
| color | string | `var(--primary-text-color)` | Default font color. Can be either hex or HA variable. Example: 'var(--secondary-text-color)'
| bnStyle | string| `var(--label-badge-blue)` | Default bar color. Can be either hex or HA variable. Example: 'var(--label-badge-green)'
| from | string | left | Direction from where the bar will start filling (must have min/max specified)
| severity | list | optional | A list of severity objects. Items in list must be ascending based on 'value'
| hideunit | boolean | optional | hide the unit of measurement if set to true. If absent, unit of measurement will be shown
| noneString | string | optional | String to use for value if value == None
| noneCardClass | string | optional | CSS class to add to card if value == None
| noneValueClass | string | optional | CSS class to add to value if value == None
| round | int | optional | Number of decimals to round to. (If not present, do not round.)
| title_color | string | color of the title. Should be in single quotes

## Examples

**Simple card**
```yaml

type: custom:andy-bignumber-card
entity: sensor.bme280_outside_temperature
title: outside
title_color: green

```

**Card with levels**

```yaml
type: custom:bignumber-card
title: Humidity
entity: sensor.outside_humidity
scale: 30px
from: bottom
min: 0
max: 100
hideunit: true
color: '#000000'
bnStyle: 'var(--label-badge-blue)'
severity:
  - value: 70
    bnStyle: 'var(--label-badge-green)'
  - value: 90
    bnStyle: 'var(--label-badge-yellow)'
  - value: 100
    bnStyle: 'var(--label-badge-red)'
    color: '#FFFFFF'
```

### Handling None values

If your sensor may result in `None` (for instance if it is offline), you may wish to handle that separately. Here is an example, which uses [card-mod](https://github.com/thomasloven/lovelace-card-mod) to add special styling for the `None` case.


```yaml
- type: custom:bignumber-card
  title: Humidity
  entity: sensor.outside_humidity
  scale: 30px
  from: bottom
  min: 0
  max: 100
  color: '#000000'
  bnStyle: 'var(--label-badge-blue)' 
  severity:
    - value: 70
      bnStyle: 'var(--label-badge-green)'
    - value: 90
      bnStyle: 'var(--label-badge-yellow)'
    - value: 100
      bnStyle: 'var(--label-badge-red)'
      color: '#FFFFFF'
  noneString: Offline
  noneCardClass: none-card-class
  noneValueClass: none-value-class
  style: |
    .none-card-class {
      background-color: yellow;
    }
    .none-value-class {
      font-size: 22px !important;
    }
```

