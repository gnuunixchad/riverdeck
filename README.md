# <img src="./misc/riverdeck-repo.png" width="24"/> riverdeck

A slightly modified version of [rivercarro], which is a slightly modifed version of _rivertile_ layout generator for
**[river-classic]**

riverdeck is the default layout generator in [my build of river-classic](https://codeberg.org/unixchad/river-classic)

Compared to _rivercarro_, _riverdeck_ adds:
-   Deck layout, master window on left, while stack windows overlap on right.

Compared to _rivertile_, _rivercarro_ adds:

-   Monocle layout, views will takes all the usable area on the screen.
-   Gaps instead of padding around views or layout area.
-   Modify gaps size at runtime.
-   Smart gaps, if there is only one view, gaps will be disable.
-   Limit the width of the usable area of the screen.
-   Per tag configurations.
-   Cycle through layout.

## Building

Same requirements as **[river-classic]**, use [zig] 0.15, if **[river-classic]** and
_rivertile_ works on your machine you shouldn't have any problems.

Build, `e.g.`

    zig build -Doptimize=ReleaseSafe --prefix ~/.local

## Usage

Works exactly as _rivertile_, you can just replace _rivertile_ name by
_riverdeck_ in your config, and read `riverdeck(1)` man page for commands
specific to riverdeck.

`e.g.` In your **river-classic** init (usually `$XDG_CONFIG_HOME/river/init`)

```bash
# Mod+H and Mod+L to decrease/increase the main ratio of riverdeck
riverctl map normal $mod H send-layout-cmd riverdeck "main-ratio -0.05"
riverctl map normal $mod L send-layout-cmd riverdeck "main-ratio +0.05"

# Mod+Shift+H and Mod+Shift+L to increment/decrement the main count of riverdeck
riverctl map normal $mod+Shift H send-layout-cmd riverdeck "main-count +1"
riverctl map normal $mod+Shift L send-layout-cmd riverdeck "main-count -1"

# Mod+{Up,Right,Down,Left} to change layout orientation
riverctl map normal $mod Up    send-layout-cmd riverdeck "main-location top"
riverctl map normal $mod Right send-layout-cmd riverdeck "main-location right"
riverctl map normal $mod Down  send-layout-cmd riverdeck "main-location bottom"
riverctl map normal $mod Left  send-layout-cmd riverdeck "main-location left"
# And for monocle
riverctl map normal $mod M     send-layout-cmd riverdeck "main-location monocle"
# And for deck
riverctl map normal $mod M     send-layout-cmd riverdeck "main-location deck"
# Cycle through layout
riverctl map normal $mod W     send-layout-cmd riverdeck "main-location-cycle left,monocle"

# Add others riverdeck's commands the same way with the keybinds you'd like.
# e.g.
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "inner-gaps -1"
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "inner-gaps +1"
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "outer-gaps -1"
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "outer-gaps +1"
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "width-ratio -0.1"
# riverctl map normal $mod <keys> send-layout-cmd riverdeck "width-ratio +0.1"

# Set the default layout generator to be riverdeck and start it.
# River-classic will send the process group of the init executable SIGTERM on exit.
riverctl default-layout riverdeck
riverdeck -outer-gaps 0 -per-tag &
```


## Thanks

Thanks to [Isaac Freund] and [Leon Henrik Plickat] for river-classic obviously, and [novakane] for rivercarro, most of riverdeck code comes from them.

Thanks to [André Desgualdo Pereira] for dwl's [decklayout] patch for reference.

## License

riverdeck is licensed under the [GNU General Public License v3.0 or later]

Files in `common/` and `protocol/` directories are released under various
licenses by various parties. You should refer to the copyright block of each
files for the licensing information.

[river-classic]: https://codeberg.org/river/river-classic
[zig]: https://ziglang.org/download/
[contributing.md]: CONTRIBUTING.md
[isaac freund]: https://codeberg.org/ifreund
[leon henrik plickat]: https://sr.ht/~leon_plickat/
[rivercarro]: https://git.sr.ht/~novakane/rivercarro
[novakane]: https://git.sr.ht/~novakane
[André Desgualdo Pereira]: https://codeberg.org/Kana
[decklayout]: https://codeberg.org/dwl/dwl-patches/src/branch/main/patches/decklayout
[gnu general public license v3.0 or later]: COPYING
