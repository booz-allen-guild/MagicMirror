# MagicMirror
MagicMirror² is an open source modular smart mirror platform. With a growing list of installable modules, the MagicMirror² allows you to convert your hallway or bathroom mirror into your personal assistant.


## Installation

### Raspbian

Raspbian is a Linux operating system designed for the Raspberry Pi. To put this onto the Raspberry Pi, we're going to need to load it onto the MicroSD card, and there are a few ways to do this.

#### Easiest Way: NOOBS

NOOBS is an operating system installer recommended by Raspberry Pi. It'll handle the installation process. Can follow the instructions here: https://www.raspberrypi.org/downloads/noobs/ (Lite version not recommended for this set up)

#### The other route: Download image and write to MicroSD

The other route is a 2 step process: Download your selected Raspbian image, then write it to your SD card using other software. 

Step 1: Download your preferred image here (Lite not recommended): https://www.raspberrypi.org/downloads/raspbian/ 

Step 2: Write the image to your SD card. A program like Etcher will write an OS image to any storage device: https://www.raspberrypi.org/documentation/installation/installing-images/README.md 

### Raspbian Set Up

Your next step is to plug your Raspberry Pi in. I tend to plug in everything except for the power supply first to make sure it has all the necessary items connected before booting up. Once it starts up, you'll be prompted with a Set Up wizard, which you'll go through and select your preferences (Time zone, language, etc). 

### MagicMirror Installation
#### Automatic Installation (Raspberry Pi only!)

*Electron*, the app wrapper around MagicMirror², only supports the Raspberry Pi 2/3. The Raspberry Pi 0/1 is currently **not** supported. If you want to run this on a Raspberry Pi 1, use the [server only](#server-only) feature and setup a fullscreen browser yourself. (Yes, people have managed to run MM² also on a Pi0, so if you insist, search in the forums.)

Note that you will need to install the latest full version of Raspbian, **don't use the Lite version**.

Execute the following command on your Raspberry Pi to install MagicMirror²:

```bash
bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh)"
```
## Modules

### API's

So the different modules use different online services to get their data. Each of those services require an API key to use. All this requires is to make an account on most occasions. We’ll just want to have these API keys/accounts created beforehand to make things a bit smoother. You’ll be able to access any web page on the raspberry pi, just like a normal PC. Why are API keys needed? Well if a developer was able to send a request freely for something without being attached to anything, they could accidentally send millions of requests and crash the site. With an API key, the site can set various limits on each user. 
 
You don’t have to sign up for every one, only the ones you’re interested in. If you have trouble signing up, we can work through it during the event. 
 
#### Weather API
- It uses OpenWeatherMap to get it’s weather data
- Sign up here: https://home.openweathermap.org/users/sign_up 
- After logged in, can go here to view and create an API Key: https://home.openweathermap.org/api_keys 
- To create a new key, provide something in the ‘Name’ field, such as ‘MagicMirror’. This is just a nickname, so does not matter what you put there. But helps keeps multiple projects in order


#### Traffic API
- We’ll utilize Google to give us up to date traffic information between 2 locations
- Go here (and login to google if you aren’t): https://developers.google.com/maps/documentation/directions/start 
- Click the ‘Get Started’ Blue button in the middle of the page. This will open a new window
- You’ll have the option to select a few products. Check the ‘Routes’ (You’ll notice it’s features include the Directions API, which we’ll utilize)
- Click Continue
- Next you’ll want to create a new project. Choose that option and give it a name, such as ‘MagicMirror’
- Next you’ll have to set a billing account (THIS WILL NOT COST ANY MONEY. So you’ll select one, but don’t worry about costs)
- Click next to Enable your APIs
- The next window you’ll see your API Key! Can copy this and store somewhere, or you’ll be able to access again from the console later on. 


#### Calendar API
- To integrate a calendar, we will be finding a .ics url for your wanted calendar
- To find your .ics link on Google, iCloud, Outlook, or some other sources, follow the instructions here: https://www.smsclientreminders.com/how_to_share_your_calendar_with_other_applications 

### Module configuration:

| **Option** | **Description** |
| --- | --- |
| `module` | The name of the module. This can also contain the subfolder. Valid examples include `clock`, `default/calendar` and `custommodules/mymodule`. |
| `position` | The location of the module in which the module will be loaded. Possible values are `top_bar`, `top_left`, `top_center`, `top_right`, `upper_third`, `middle_center`, `lower_third`, `bottom_left`, `bottom_center`, `bottom_right`, `bottom_bar`, `fullscreen_above`, and `fullscreen_below`. This field is optional but most modules require this field to set. Check the documentation of the module for more information. Multiple modules with the same position will be ordered based on the order in the configuration file. |
| `classes` | Additional classes which are passed to the module. The field is optional. |
| `header` | To display a header text above the module, add the header property. This field is optional. |
| `disabled` | Set disabled to `true` to skip creating the module. This field is optional. |
| `config` | An object with the module configuration properties. Check the documentation of the module for more information. This field is optional, unless the module requires extra configuration. |

The following modules are installed by default.

- [**Clock**](modules/default/clock)
- [**Calendar**](modules/default/calendar)
- [**Current Weather**](modules/default/currentweather)
    - City of Saint Louis - 4407084
- [**Weather Forecast**](modules/default/weatherforecast)
    - City of Saint Louis - 4407084
- [**News Feed**](modules/default/newsfeed)
- [**Compliments**](modules/default/compliments)
- [**Hello World**](modules/default/helloworld)
- [**Alert**](modules/default/alert)

For more available modules, check out out the wiki page [MagicMirror² 3rd Party Modules](https://github.com/MichMich/MagicMirror/wiki/3rd-party-modules). If you want to build your own modules, check out the [MagicMirror² Module Development Documentation](modules) and don't forget to add it to the wiki and the [forum](https://forum.magicmirror.builders/category/7/showcase)!

### 3rd Party Modules

[MMM-Traffic](https://github.com/SamLewis0602/MMM-Traffic)

## Additional Set Up

### Auto Start (Ideally do this step last after everything is set up)

- Option 1 (Recommended if you want to tweak Raspberry Pi stuff afterwards)

This option tells Raspberry Pi to run the MagicMirror start command when it boots up.

````
crontab -e
````
Add the commands at the bottom:
````
@reboot npm start /home/pi/MagicMirror
````
Save the changes
````
ctrl+o
````
Exit the editor
````
ctrl+x
````

- Option 2 (Recommended if you're only using this for MagicMirror, and never want to deal with the rest)
[MagicMirror Recommended Way](https://github.com/MichMich/MagicMirror/wiki/Auto-Starting-MagicMirror)



### Rotate Screen

edit _/boot/config.txt_:
````
sudo nano /boot/config.txt
````
Add the following line:
````
display_rotate=1
avoid_warnings=1 
````
> #display_rotate=0 Normal

> #display_rotate=1 90 degrees

> #display_rotate=2 180 degrees

> #NOTE: You can rotate both the image and touch interface 180º by entering lcd_rotate=2 instead`

> #display_rotate=3 270 degrees

Then reboot the pi:
````
sudo reboot
````

### Hide Mouse

Install _unclutter_: 
````
sudo apt-get install unclutter
````
You can create an `.xinitrc` script to run the tool.  
See https://wiki.archlinux.org/index.php/Unclutter

But a simpler option is to add a line to the end of the file:

```bash
$ nano ~/.config/lxsession/LXDE-pi/autostart
...
@unclutter -display :0 -idle 3 -root -noevents
```
This will add a 3 second delay, before the pointer disappears from the screen when not using it.

### Disable Screensaver

Unfortunately by default, Raspbian has no way to control the screensaver. Install xscreensaver to control it:
````
sudo apt-get install xscreensaver
````

After install, click on the Raspberry Pi Start Menu in upper left > Preferences > Screensaver

In the Mode drop down menu, select 'Disable Screen Saver'

## MagicMirror Construction

- [**Tapp Plastics**](https://www.tapplastics.com/product/plastics/cut_to_size_plastic/two_way_mirrored_acrylic/558)
  
  1/8 (.118) inches Thick, 14 inches Wide, 24 inches Long
  
- [Custom Two Way Mirror Vendors](https://github.com/MichMich/MagicMirror/wiki/Two-way-Mirror-Vendors)
