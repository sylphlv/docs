# Theme inheritance configuration

## Overview

This guide explains how you can use a theme as a basic corporate design theme and create inherited themes for 
special purposes like holiday time or a sales week.

Imagine you have a theme which is applying your corporate design to the storefront. With your colors, your logo and 
other configuration fields. But on a special week in the year you have additional requirements for a special design, 
like a discount counter or an advent calender.  

## Prerequisites

1. Create the two themes like descriped in [Theme inheritance](./add-theme-inheritance.md).
2. Add some configuration fields you need in your basic theme inside the `theme.json` of the `SwagBasicExampleTheme`
   {% code title="<plugin root>/src/Resources/theme.json" %}
```javascript
{
  "name": "SwagBasicExampleTheme",
  .....
  "config": {
    "blocks": {
      "colors": {
        "themeColors": {
          "en-GB": "Theme colours",
          "de-DE": "Theme Farben"
        }
      }
    },
    "sections": {
      "importantColors": {
        "label": {
          "en-GB": "Important colors",
          "de-DE": "Wichtige Farben"
        }
      }
    },
    "tabs": {
      "colors": {
          "label": {
              "en-GB": "Colours",
              "de-DE": "Farben"
          }
      } 
    },
    "fields": {
      "sw-color-brand-primary": {
        "label": {
          "en-GB": "Primary colour",
          "de-DE": "Primär"
        },
        "type": "color",
        "value": "#399",
        "editable": true,
        "tab": "colors",
        "block": "themeColors",
        "section": "importantColors"
      },
      "sw-brand-icon": {
        "label": {
            "en-GB": "Brand icon", 
            "de-DE": "Markenlogo"
        },
        "type": "url",
        "value": "/our-logo.png",
        "editable": true
      }
    }
  }
}
```
{% endcode %}

## Extending an existing theme configuration with a new theme

Add configurations to your extended theme
   {% code title="<plugin root>/src/Resources/theme.json" %}
```javascript
{
  "name": "SwagBasicExampleThemeExtend",
  .....
  "configInheritance": {
    "@Storefront",
    "@SwagBasicExampleTheme"
  },
  "config": {
    "fields": {
      "sw-brand-icon": {
        "type": "url",
        "value": "/our-logo-holidays.png",
        "editable": true
      },
      "sw-advent-calender-background-color": {
        "label": {
          "en-GB": "Advent calender background color",
          "de-DE": "Adventskalender Hintergrundfarbe"
        },
        "type": "color",
        "value": "#399",
        "editable": true
      }
    }
  }
}
```

In this theme (`SwagBasicExampleThemeExtend`) all the configuration fields from the themes `Storefront` and 
`SwagBasicExampleTheme` will be used as inherited values. They will be shown in the administration with an inherit 
anchor and will use the value of the parent themes as long as they are not set to a different value.
In the `theme.json` the `sw-brand-icon` field value will be overwritten with a different default value. So this field 
will not be inherited regardless that it is already defined in the `SwagBasicExampleTheme`. This theme also adds a 
new field for the background color of the advent calender (`sw-advent-calender-background-color`) because this is 
only needed in this special theme which will only be used for 4-6 weeks a year.

## Next steps

Now that you know how the theme inheritance works you can start with own customizations. Here is a list of other related topics where assets can be used.

* [Add SCSS Styling and JavaScript to a theme](add-css-js-to-theme.md)
* [Customize templates](../plugins/storefront/customize-templates.md)

