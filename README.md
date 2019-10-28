# i3-keyboard-layout

Change keyboard layout with a keystroke + show it in the status bar.

## Install

Download `i3-keyboard-layout`, make sure it's executable (`chmod + x <file>`), and store it somewhere in your home directory (or in your `$PATH` if you prefer)

## Usage

Assign a keystroke in your [i3](https://i3wm.org/) configuration to switch to different layouts:

```
# ~/.config/i3/config

bindsym $mod+z exec path/to/i3-keyboard-layout set us
bindsym $mod+x exec path/to/i3-keyboard-layout set es
```

Alternatively (or aditionally), you can use a single keystroke to cycle through a list of your most used layouts:


```
# ~/.config/i3/config

bindsym $mod+space exec path/to/i3-keyboard-layout cycle us es de
```

Each time you press that key, the next layout on the list will be selected.

If you want to use layouts with variants, you can use quotes, like this:

```
# ~/.config/i3/config

bindsym $mod+space exec path/to/i3-keyboard-layout cycle us "us euro"
```

## Display current layout

**NOTE:** You can skip this part if you use some kind of tray indicator such as [sbxkb](https://www.archlinux.org/packages/community/x86_64/sbxkb/), which is probably what you want if you prefer a flag instead of the name of the layout.

A subcommand is included to display the current layout on the `i3status` bar. On your bar configuration, you need to pipe `i3status` onto the `i3status` subcommand:


```
# ~/.config/i3/config

bar {
  # status_command i3status # this is the usual default configuration
  status_command i3status | i3-keyboard-layout i3status
}
```
`i3status` needs to be configured tou output the `i3bar` JSON format (which is usually the default):

```
# ~/.config/i3status/config

general {
  output_format = i3bar
}
```

At this point only prepending the layout at the left of everything else is supported.

![i3 bar](screenshot.png)
