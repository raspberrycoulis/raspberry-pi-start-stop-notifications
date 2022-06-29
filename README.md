# raspberry-pi-start-stop-notifications
A basic script that generates a push notification via Pushover when the Raspberry Pi boots and shuts down

## What this does
This is a very basic shell script, based on the one found [here](https://raspberrypi.stackexchange.com/questions/1531/how-do-i-set-up-pushover-service-to-tell-me-when-my-pi-is-shutting-down-or-start), which generates a push notification - via [Pushover](https://pushover.net) - when a Raspberry Pi (or other Linux based system) boots or shuts down.

## How to install
To run this script automatically on boot / shutdown, the script needs to be placed in `/etc/init.d/` with the correct permissions (see below for details). You can either clone this repository and move the `pushover` script to the above location, or create it yourself in the directory via your preferred text editor.

You'll also need two API tokens from your Pushover account for the script to work:

1. User token (from your Pushover account)
2. App token (from the app you'll need to create in your Pushover account)

These tokens need to be included in the relevant parts of the script - i.e.:

```bash
TOKEN=something-random-and-secret
USER=something-else-random-and-secret
```

Assuming your script is called `pushover` and located in `/etc/init.d/`, the following commands are needed to allow the script to run on boot / shutdown:

```bash
sudo chmod 755 /etc/init.d/pushover
sudo chown root:root /etc/init.d/pushover
sudo update-rc.d pushover defaults
```

##  Customising the Pushover notification
The current message is quite straight forward and says "Raspberry Pi (hostname) has just booted." / "Raspberry Pi (hostname) is shutting down." The `hostname` is a variable that will be pulled from the hostname your Raspberry Pi has been given, and this can be changed in the `raspi-config` menu.

The sound the notification makes can also be changed. By default it uses the `gamelan` sound effect - a standard Pushover notification sound - but it can use any of the supported notification sounds found in the [Pushover API documentation](https://pushover.net/api#sounds). If you have uploaded your own custom alert sounds, they are [also supported](https://blog.pushover.net/posts/2021/3/custom-sounds) - you'll just need to change the following snippet in the script:

```bash
SOUND=gamelan
```
