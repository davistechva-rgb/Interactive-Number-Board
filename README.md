Overview

Number Board turns any TV or projector into a live draw board. You run the game from a control panel on a phone, tablet, or laptop, and each number you call animates off every display at the same time. When the last number is called, the board announces it as the winner with a confetti celebration.

It's built as two simple web pages connected through Ably, a real-time messaging service with a free tier. There's nothing to install and no server to run. Host the files anywhere, open them in a browser, and enter your key once on each device.

Features

Display (index.html)

Full-screen number grid that sizes itself to fit any screen
Called numbers flash and dim on the board as they're pulled
Remaining, Called, and Total counters
Last 5 numbers called, newest first
Event title across the top, set from the control panel
Winner screen with confetti when every number has been called, cleared automatically when the board is reset
Late joiners catch up: a display that's opened or refreshed mid-game jumps straight to the current board
Connection light in the corner that turns green when live
Works on several screens at once

Control panel (control-panel.html)

Set up any board: title, up to 500 numbers, and any starting number
Tap to call: select numbers on the board and remove them
Remove Random calls a random batch of 1, 5, 10, 15, or 25
Restore All Numbers starts a new game
Live/Offline badge so you always know the displays are receiving updates
Phone-friendly layout

Security

No keys in the code. Keys are entered on each device and saved only in that browser, so the project can be shared publicly without exposing them.
Setup
1. Get your Ably keys
Create a free account at ably.com and create an app.
Under API Keys, create two keys:
Key	Permissions	Used on
Display key	Subscribe and History	Every screen showing the board
Control key	Publish, Subscribe, and History	Only the device running the game

History lets a display that opens late catch up to the current game. It can only read, never change anything.

2. Host the files

Upload the folder to any static host, such as Netlify, GitHub Pages, or your own website. The files contain no keys, so they can be published as-is.

3. Connect the control panel
Open control-panel.html on your phone, tablet, or laptop.
On the Setup tab, paste your control key under Connection and tap Save & Connect.
The badge changes to Live. The key is remembered on that device.
4. Connect each display
Open index.html on the computer connected to the TV or projector.
Paste your display key when asked and tap Connect.
Go full screen: F11 on Windows, Ctrl+Cmd+F on Mac.

Tip: to skip typing on a display computer, open the board once with the key in the address, such as https://your-site.netlify.app/?key=YOUR_DISPLAY_KEY. The board saves it and removes it from the address bar right away.

5. Run the game
On the control panel's Setup tab, enter the title, total numbers, and starting number, then tap Rebuild Board. The displays switch to the live board.
Call numbers from the Board tab by tapping them, or use Remove Random on the Actions tab.
When the last number is called, the displays show the winner.
Tap Restore All Numbers to start over.
Good to know
Keys are saved per browser. Each new device or browser asks for a key once. Use Forget Key on the control panel, or open the board with ?forget at the end of the address, to remove a saved key.
Only enter the control key on devices you trust. Anyone with it can run the board.
Separate events: both pages use the channel numberboard-v1 by default. Add ?channel=your-event-name to the address of both pages to keep a new event separate from old games.
An internet connection is needed on every device during the game.
If a key is exposed, revoke it in the Ably dashboard and create a new one.
Project files
File	Purpose
index.html	The display board for TVs and projectors
control-panel.html	The controller for running the game
README.md	This guide
LICENSE	MIT License
Customizing

Each page has a Theme section of color settings at the top of its <style> block. Change those values to match your event's colors.

How it works

The control panel publishes a message named state on the Ably channel <channel>:state every time something changes. Each display subscribes to that channel and redraws to match. The message looks like this:

json
{
  "title": "Spring Raffle",
  "total": 400,
  "start": 1,
  "removed": ["0", "17", "254"],
  "lastCalledLog": [18, 255, 1]
}
Field	Meaning
title	Heading shown on the display
total	How many numbers are on the board
start	The first number (the board shows start through start + total - 1)
removed	Positions (0-based) of numbers already called
lastCalledLog	Numbers called, in order. The last one is the most recent
License

Released under the MIT License. Copyright © 2026 Davis Tech Support (Michael Davis).

You're free to use, copy, modify, and share this project, including in commercial work, as long as the copyright and license notice stay with it.

Contributing

Bug reports, ideas, and pull requests are welcome. Open an issue to describe what you found or what you'd like to add.

Contact

Davis Tech Support, IT consulting and managed services in Central Virginia

Website: davis-tech-support.com
Email: davis.tech.va@gmail.com
Phone/Text: 434-294-4456

For custom versions, event setup, or support, get in touch.
