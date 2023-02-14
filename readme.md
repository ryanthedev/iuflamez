## i3 Ubuntu Flameshot
### OHHH YEA

so...on my journey to rice out my linux, i found the need to take screenshots.
well the need was so i can post and make dank memes for tech twitter, but
tomato, potato.

fist thing was finding a cool screen shot tool.  flameshot.org came in clutch.
this provides like 99% of what you need, but we want to be uncommon amongst
the uncommon (thankz goggins).

first thing i wanted to do was configure a bind in i3 to launch flameshot in 
drag mode. ezpz

go to your i3 config...
```i3config
bindsym $mod+Print exec --no-startup-id flameshot gui
```
reload your i3 and BOOM..SCREENSHOT. (FYI - i set this up to work with my powerfinger *mod*
and print screen button). if future self wants something else..have at it.

---
### cool.cool.cool.
let's kick it up a notch, eh?
what if i want to screenshot my current active window?
well thanks to google and some hardcore nerds you can do that.

first you need a tool called `xdotool`
cool.  do your install thingy.  wait.  wtf is this thing?
well after you install you can man it. `man xdotool` (i love linux)

tl;dr;
it's a remote workers wet dream.

---

i grabbed this script from the flameshot github issues (u da man zeorin)

``` bash
#!/bin/bash

if [ "$1" = "activewindow" ]; then
  # get active window geometry
  eval $(xdotool getactivewindow getwindowgeometry --shell)
  REGION="${WIDTH}x${HEIGHT}+${X}+${Y}"
elif [ "$1" = "selectwindow" ]; then
  # let user select a window then you know..
  eval $(xdotool selectwindow getwindowgeometry --shell)
  REGION="${WIDTH}x${HEIGHT}+${X}+${Y}"
else
  # get current screen
  SCREEN=$(xdotool get_desktop)
  REGION="screen${SCREEN}"
fi

# launch flameshot
flameshot gui --region "$REGION"
```

ohhh...magik
---
noice.  now i wanted to execute this script as part of my i3 sweetness.  so i need to place
the script somewhere and add that somewhere to my path so that way i don't need to add paths 
and stuffz.  

i opted to place the script in my `$HOME/bin` and added that to my `.zshrc`

like so
``` zsh
export PATH=$PATH:$HOME/bin
```
next you need to add some things to your i3 config.

i wanted to use my power finger and some combo of another finger and print scrn.  so...

``` i3
# screenshots
bindsym $mod+Print exec --no-startup-id flameshot gui
bindsym $mod+Control+Print exec --no-startup-id master_flamez.sh activewindow 
bindsym --release $mod+Shift+Print exec --no-startup-id master_flamez.sh selectwindow 
```

i have the `--release` because you need it.  also you can see what i named my script.
if you have more questions about why i put what i did, don;t ask. i have no idea. copy
pasta.













