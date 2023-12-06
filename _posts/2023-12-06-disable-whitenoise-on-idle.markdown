---
layout: post
title:  "Disabling pipewire whitenoise on idle"
tags: pipewire wireplumber
---

I'm writing this here so I "don't forget".

My speakers emit a annoying whitenoise when they are turned on but there's no signal, the problem is that my ArchLinux setup
is putting the sound board into idle mode to save power after 3 (or 5?) seconds, so every time I stop listeing something,
after 3 (or 5?) seconds the whitenoise starts... really annoying.

I fixed this once, but I was lazy enough to edit system files instead of user files, so today I updated wireplumber again
and the whitenoise was back there.

To let you and future me repeat the same mistake of present mine, if this happen to you, edit these files:

Comment this line from `/usr/share/wireplumber/main.lua.d/90-enable-all.lua`:

```lua
-- Automatically suspends idle nodes after 3 seconds
--load_script("suspend-node.lua")
```

Restart wireplumber:

```
systemctl --user restart wireplumber
```

Months ago I had also to edit `/usr/share/wireplumber/main.lua.d/50-alsa-config.lua`

Uncomment this line at end and set the value to 0 as the comment says.

```lua
--["session.suspend-timeout-seconds"] = 0,  -- 0 disables suspend
```

But nowadays the 90-enable-all.lua seems enough.
