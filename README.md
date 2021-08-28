# Bismuth

This is a fork of [Krohnkite](https://github.com/esjeon/krohnkite) - a dynamic tiling extension for KWin.

## Features

- DWM-like window tiling
  - Dynamically tile windows, rather than manually placing each.
  - Floating windows
- Fully integrates into KWin features, including:
  - **Multi-screen**
  - **Activities & Virtual desktop**
  - Basic window management (minimize, fullscreen, switching, etc)
- Multiple Layout Support
  - Tiling layout
  - Monocle layout
  - Desktop-friendly layouts (Spread, Stair)

## Development Requirement

- NPM
- p7zip (7z)

## Installation


    make install
    make uninstall # to uninstall the script

## Simply Trying Out

Bismuth can be temporarily loaded without installing the script:

    make run
    make stop

Note that Bismuth can destroy itself completely once it is disabled, so no
restart is required to deactivated it.

### Enabling User-Configuration

[It is reported][kwinconf] that a manual step is required to enable user
configuration of KWin scripts. This is a limitation of KWin scripting.

To enable configuration, you must perform the following in command-line:

    mkdir -p ~/.local/share/kservices5/
    ln -s ~/.local/share/kwin/scripts/bismuth/metadata.desktop ~/.local/share/kservices5/bismuth.desktop

A configuration button will appear in `KWin Scripts` in `System Settings`.

![config button shown](img/conf.png)

To make changes effective, **the script must be reactivated**:

1. On `KWin Scripts` dialog, untick Bismuth
2. `Apply`
3. tick Bismuth
4. `Apply`

[kwinconf]: https://github.com/faho/kwin-tiling/issues/79#issuecomment-311465357

## Default Key Bindings

| Key              | Action             |
| ---------------- | ------------------ |
| Meta + J         | Focus Down/Next    |
| Meta + K         | Focus Up/Previous  |
| Meta + H         | Left               |
| Meta + L         | Right              |
|                  |                    |
| Meta + Shift + J | Move Down/Next     |
| Meta + Shift + K | Move Up/Previous   |
| Meta + Shift + H | Move Left          |
| Meta + Shift + L | Move Right         |
|                  |                    |
| Meta + I         | Increase           |
| Meta + D         | Decrease           |
| Meta + F         | Toggle Floating    |
| Meta + \         | Cycle Layout       |
|                  |                    |
| Meta + Return    | Set as Master      |
|                  |                    |
| Meta + T         | Use Tile Layout    |
| Meta + M         | Use Monocle Layout |
| _unbound_        | Use Spread Layout  |
| _unbound_        | Use Stair Layout   |

## Tips

### Setting Up for Multi-Screen

Bismuth supports multi-screen setup, but KWin has to be configured to unlock
the full potential of the script.

1. Enable `Separate Screen Focus` under `Window Management` >
   `Window Behavior` > `Multiscreen Behaviour`
2. Bind keys for global shortcut `Switch to Next/Previous Screen`
   (Recommend: `Meta + ,` / `Meta + .`)
3. Bind keys for global shortcut `Window to Next/Previous Screen`
   (Recommend: `Meta + <` / `Meta + >`)

Note: `Separate Screen Focus` appears only when multiple monitors are present.

### Removing Title Bars

Breeze window decoration can be configured to completely remove title bars from
all windows:

1. `System Setting` > `Application Style` > `Window Decorations`
2. Click `Configure Breeze` inside the decoration preview.
3. `Window-Specific Overrides` tab > `Add` button
4. Enter the followings, and press `Ok`:
   - `Regular expression to match`: `.*`
   - Tick `Hide window title bar`

### Changing Border Colors

Changing the border color makes it easier to identify current window. This is
convenient if title bars are removed.

1.  Open `~/.config/kdeglobals` with your favorite editor
2.  Scroll down and find `[WM]` section
3.  Append the followings to the section:

    - `frame=61,174,233`: set the border color of active window to _RGB(61,174,233)_
    - `inactiveFrame=239,240,241`: set the border color of inactive window to _RGB(239,240,241)_

    Here's a nice 2-liner that'll do it for you:

         kwriteconfig5 --file ~/.config/kdeglobals --group WM --key frame 61,174,233
         kwriteconfig5 --file ~/.config/kdeglobals --group WM --key inactiveFrame  239,240,241

4.  You must **restart** your session to see changes. (i.e. re-login, reboot)

Note: the RGB values presented here are for the default Breeze theme

Note: You might also need to set the border size larger than the theme's default:
`System Settings` > `Application Style` > `Window Decorations`: Untick `Use theme's default window border size` and adjust the size (right from the checkbox).

### Setting Minimum Geometry Size

Some applications like discord and KDE settings don't tile nicely as they have a minimum size requirement.
This causes the applications to overlap with other applications. To mitigate this we can set minimum size for all windows to be 0.

1. `System Setting` > `Window Management` > `Window Rules`
2. Click on `+ Add New...`
3. Set `Window class` to be `Unimportant`
4. Set `Window types` to `Normal Window`
5. Click `+ Add Properties...`
6. Add the `Minimum Size` Property
7. Set the fields to `Force` and `0` x `0`
8. Apply

