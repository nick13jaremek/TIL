# Problem

When working with Linux on a laptop computer with a touchpad, it could happen that when resuming after suspending, the touchpad does not respond (i.e. does not work). 

# Solution

The issue can be resolved by forcing a reload of the touchpad / mouse drivers. To make this more automatic (i.e. reload after resuming a suspended laptop), a script can be added.

This script will be executed after each suspend resume.

1. Create a new file for the script: `sudo vim /lib/systemd/system-sleep/touchpad`
2. Add the following content to the script file:
```
#!/bin/bash

if [[ $1 == post ]]; then
    modprobe -r psmouse
    modprobe psmouse
fi
```
3. Add execution permissions to this new script: `sudo chmod a+x /lib/systemd/system-sleep/touchpad`

## Important

Restart your computer for this script to be executed from now on after a suspend resume.
