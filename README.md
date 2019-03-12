# MagicMirror
MagicMirror² is an open source modular smart mirror platform. With a growing list of installable modules, the MagicMirror² allows you to convert your hallway or bathroom mirror into your personal assistant.


## Installation

### Raspberry Pi

#### Automatic Installation (Raspberry Pi only!)

*Electron*, the app wrapper around MagicMirror², only supports the Raspberry Pi 2/3. The Raspberry Pi 0/1 is currently **not** supported. If you want to run this on a Raspberry Pi 1, use the [server only](#server-only) feature and setup a fullscreen browser yourself. (Yes, people have managed to run MM² also on a Pi0, so if you insist, search in the forums.)

Note that you will need to install the latest full version of Raspbian, **don't use the Lite version**.

Execute the following command on your Raspberry Pi to install MagicMirror²:

```bash
bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh)"
```

Module configuration:

| **Option** | **Description** |
| --- | --- |
| `module` | The name of the module. This can also contain the subfolder. Valid examples include `clock`, `default/calendar` and `custommodules/mymodule`. |
| `position` | The location of the module in which the module will be loaded. Possible values are `top_bar`, `top_left`, `top_center`, `top_right`, `upper_third`, `middle_center`, `lower_third`, `bottom_left`, `bottom_center`, `bottom_right`, `bottom_bar`, `fullscreen_above`, and `fullscreen_below`. This field is optional but most modules require this field to set. Check the documentation of the module for more information. Multiple modules with the same position will be ordered based on the order in the configuration file. |
| `classes` | Additional classes which are passed to the module. The field is optional. |
| `header` | To display a header text above the module, add the header property. This field is optional. |
| `disabled` | Set disabled to `true` to skip creating the module. This field is optional. |
| `config` | An object with the module configuration properties. Check the documentation of the module for more information. This field is optional, unless the module requires extra configuration. |

## Modules

The following modules are installed by default.

- [**Clock**](modules/default/clock)
- [**Calendar**](modules/default/calendar)
- [**Current Weather**](modules/default/currentweather)
- [**Weather Forecast**](modules/default/weatherforecast)
- [**News Feed**](modules/default/newsfeed)
- [**Compliments**](modules/default/compliments)
- [**Hello World**](modules/default/helloworld)
- [**Alert**](modules/default/alert)

For more available modules, check out out the wiki page [MagicMirror² 3rd Party Modules](https://github.com/MichMich/MagicMirror/wiki/3rd-party-modules). If you want to build your own modules, check out the [MagicMirror² Module Development Documentation](modules) and don't forget to add it to the wiki and the [forum](https://forum.magicmirror.builders/category/7/showcase)!
