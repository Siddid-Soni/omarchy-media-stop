# Media Stop for Omarchy

Omarchy's built-in media service and bar widget, with a working **Stop** key
that behaves like it does on Windows: stopping a player releases it, and the
media keys move on to the next player.

- **Stop** sends a real MPRIS Stop to the current player and drops it from
  media-key control. The OSD shows a square stop icon.
- **Play/pause, next and previous** then go to the next player, playing or
  paused. The stopped player also leaves the bar widget.
- **Browsers:** Chromium-based browsers (Brave, Chrome, Chromium) show all
  their tabs as one player. A real Stop makes the browser drop that tab's
  session and switch its player to the next media tab, which the keys then
  control.
- A stopped player comes back under media-key control as soon as it plays
  again from its own app, or switches to a different track.

Everything else is the stock Omarchy media plugin, unchanged.

## Install

```bash
omarchy plugin add https://github.com/Siddid-Soni/omarchy-media-stop.git --enable
```

This takes over from the built-in `omarchy.media` (bar widget and the
`omarchy-shell media ...` commands). If the bar placement prompt doesn't put it
where the old media widget was, move it with
`omarchy bar move io.github.siddid-soni.media-stop --section center`.

### Bind the Stop key

Omarchy doesn't bind the Stop key, and plugins can't add keybindings, so add
this to `~/.config/hypr/bindings.lua`:

```lua
o.bind("XF86AudioStop", "Stop", "omarchy-shell media stop", { locked = true })
```

Hyprland reloads on save. If your keyboard's Stop key sends a different key,
run `wev`, press it, and use the key name it prints.

You can also run `omarchy-shell media stop` from a script or another binding.

## Uninstall

```bash
omarchy plugin remove io.github.siddid-soni.media-stop
```

This puts the built-in Omarchy media plugin back. Remove the `XF86AudioStop`
line from `bindings.lua` too.

## Notes

- Based on the media plugin from Omarchy 4.0.4. Changes Omarchy makes to its
  built-in media plugin later won't show up here until this plugin is updated.
- Stop is a real stop, so players that support it reset to the start of the
  track. Players that refuse media commands are paused instead.

## License

MIT. Contains code from [Omarchy](https://github.com/basecamp/omarchy),
copyright David Heinemeier Hansson, also MIT.
