# rvclient-linux

A setup tool that gets Rumbleverse running on Linux through Proton, using the
rVclient community client.

You bring your own game files. Everything else is done for you.

## What it does

- Finds your Rumbleverse folder, or unpacks it if you still have it as a zip.
- Downloads the newest rVclient client files and puts them in the right place.
- Makes your player name into an account on the rVclient backend.
- Shows the live server list and lets you pick where to play.
- Prints the exact Steam launch options to paste in.

Run it again whenever you want to play somewhere else. It remembers everything
else.

## Requirements

- A 64-bit Linux desktop.
- Steam, with Proton available under Compatibility.
- Your own Rumbleverse game files, as a folder or a zip.
- `curl` for the one-step command below.

## Setup

Paste this into a terminal. It downloads the tool, puts it in `~/.local/bin`,
and runs it.

```sh
mkdir -p ~/.local/bin
curl -fsSL -o ~/.local/bin/rvclient-linux \
  https://github.com/cmspam/rvclient-linux/releases/latest/download/rvclient-linux
chmod +x ~/.local/bin/rvclient-linux
~/.local/bin/rvclient-linux
```

If `~/.local/bin` is not on your `PATH`, run it by full path, or add this to
your shell profile:

```sh
export PATH="$HOME/.local/bin:$PATH"
```

## Playing

The tool prints a line to paste into Steam. In short:

1. In Steam, right-click Rumbleverse and choose **Properties**.
2. On the **General** tab, paste the line into **Launch Options**.
3. On the **Compatibility** tab, tick **Force the use of a specific Steam Play
   compatibility tool** and choose a Proton version.
4. Press **Play**.

The first start takes a minute or so while Proton prepares its prefix. Later
starts are quick.

## Changing server

Run the tool again:

```sh
~/.local/bin/rvclient-linux
```

Pick a different server and paste the new launch options into Steam. Pressing
Enter at the server question keeps the one you already have.

## What it writes

| File | What it is |
|---|---|
| `rVclient.ini` | Your settings, in the same format the rVclient launcher uses |
| `credentials.dat` | Your account token, readable only by you |

Both sit next to the `rvclient-linux` binary. If you move the binary, move
these with it, or the tool will make you a new account.

The launch options the tool prints contain your account token, so treat them
the way you would a password.

## Notes

- Your account token is what makes the game use your account instead of
  appearing as a guest. It is passed to the game through the Steam launch
  options, which is the same way the launcher passes it on Windows.
- `WINEDLLOVERRIDES="dxgi=n,b"` in those options is what lets the client load
  its own `dxgi.dll`. Without it, many features will not work.
- The tool talks to the same backend the rVclient launcher uses, so the server
  list and player counts are the live ones.

## Source code

Not published yet. The source will be made available when rvclient itself goes
open source.

## Credits

- rVclient, the community client and backend: [techwhipped/rvclient-updates](https://github.com/techwhipped/rvclient-updates)
- Community: [discord.gg/rvclient](https://discord.gg/rvclient)

Rumbleverse is a game by Iron Galaxy Studios and Epic Games. This tool is
unofficial and is not affiliated with either of them.
