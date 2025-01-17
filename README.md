# Chromium kiosk

Chromium kiosk is simple package turning your Linux based PC/Raspberry into simple web kiosk using chromium.

# Features

* Simple installation and configuration
* Installed from repository
* Restarts whole machine when chromium process crashes/exists
* Tested on Archlinux, Archlinux ARM, Debian, Raspbian
* Integrated virtual keyboard (via chromium extension)
* Integrated whitelist (via chromium extension)
* Redirect to homepage when idle for specified amount of time
* Show screen saver when idle for specified amount of time

# Installation

## Archlinux
(Use Archlinux ARM for Raspberry install)

Add repository by adding this at end of file /etc/pacman.conf

```
[salamek]
Server = https://repository.salamek.cz/arch/pub/any
SigLevel = Optional
```

and then install by running

```bash
$ pacman -Sy chromium-kiosk
```

after that you can reboot your device, you should be welcomed by `chromium-kiosk` welcome page:
```bash
$ reboot
```

# Debian and derivates
(For Raspbian i suggest to use Lite relase)

Add repository by running these commands

```bash
$ wget -O - https://repository.salamek.cz/deb/salamek.gpg.key|sudo apt-key add -
$ echo "deb     https://repository.salamek.cz/deb/pub all main" | sudo tee /etc/apt/sources.list.d/salamek.cz.list
```

And then you can install a package `chromium-kiosk`

```bash
$ apt update && apt install chromium-kiosk
```

after that you can reboot your device, you should be welcomed by `chromium-kiosk` welcome page:
```bash
$ reboot
```

# Setup

After successful installation you will want to configure `chromium-kiosk` by editing `/etc/chromium-kiosk/config.yml`, these are the options:

```yml
CLEAN_START: true  # Force chromium to clean start on each boot (That simply means do not show "Restore pages" dialog, you want this to be true in 99% of use cases)
KIOSK: true # Run in kiosk mode, chromium will use whole screen without any way for user to close it, setting this to false is useful for web application debug (you can access chromium Inspect tool and so on) and initial chromium configuration
TOUCHSCREEN: true # Enables support for touchscreen
HOME_PAGE: 'https://salamek.github.io/chromium-kiosk/'  # Url to load as homepage

# These works only with chromium-kiosk installed
IDLE_TIME: 0 # How log must be kiosk idle to redirect to HOME_PAGE, 0=disabled (Works only with chromium-kiosk extension installed)
WHITE_LIST:
  ENABLED': false  # is white list enabled
  URLS': []   # List of whitelisted urls, glob format is supported (eg,: *,google.*/news)
  IFRAME_ENABLED': true  # True to enable all iframes, list of urls to specify enabled iframes

NAV_BAR:
  ENABLED: false # is nav bar enabled
  ENABLED_BUTTONS: ['home', 'reload', 'back', 'forward'] # Enabled buttons on navbar, order matters
  HORIZONTAL_POSITION: 'center' # horizontal position on the screen
  VERTICAL_POSITION: 'bottom' # Vertical position on the screen
  WIDTH: 100 # Width of a bar in %

VIRTUAL_KEYBOARD:
  ENABLED: false # is virutal keyboard enabled

SCREEN_SAVER:
  ENABLED: false  # is screen saver enabled
  IDLE_TIME: 0  # how long must be a user idle for screensaver to start
  TEXT: 'Touch me'
  
DISPLAY_ROTATION: 'normal' # Rotates display when X server starts options are (normal|left|right|inverted)
#SCREEN_ROTATION: 'normal'  Rotates screen individually (do not rotate touchscreen) when X server starts options are (normal|left|right|inverted), remove DISPLAY_ROTATION for this to work
#TOUCHSCREEN_ROTATION: 'normal'  Rotates touchscreen individually (do not rotate screen) when X server starts options are (normal|left|right|inverted), remove DISPLAY_ROTATION for this to work
```
