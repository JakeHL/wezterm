# SwitchToWorkspace

*Since: 20220319-142410-0fcdea07*

Switch to a different workspace, creating it if it doesn't already exist.

`SwitchToWorkspace` accepts two optional parameters:

* `name` - the name of the workspace. If omitted, a randomly generated name will be chosen.
* `spawn` - a [SpawnCommand](../SpawnCommand.md) describing the command that should be started in the workspace if it doesn't already exist.  If omitted, the default program will be spawned in the newly created workspace.

```lua
local wezterm = require 'wezterm'
local act = wezterm.action

wezterm.on('update-right-status', function(window, pane)
  window:set_right_status(window:active_workspace())
end)

return {
  keys = {
    -- Switch to the default workspace
    {
      key = 'y',
      mods = 'CTRL|SHIFT',
      action = act.SwitchToWorkspace {
        name = 'default',
      },
    },
    -- Switch to a monitoring workspace, which will have `top` launched into it
    {
      key = 'u',
      mods = 'CTRL|SHIFT',
      action = act.SwitchToWorkspace {
        name = 'monitoring',
        spawn = {
          args = { 'top' },
        },
      },
    },
    -- Create a new workspace with a random name and switch to it
    { key = 'i', mods = 'CTRL|SHIFT', action = act.SwitchToWorkspace },
    -- Show the launcher in fuzzy selection mode and have it list all workspaces
    -- and allow activating one.
    {
      key = '9',
      mods = 'ALT',
      action = act.ShowLauncherArgs {
        flags = 'FUZZY|WORKSPACES',
      },
    },
  },
}
```

