---
title: "Linux Terminal Shortcuts"
date: 2020-03-30T04:17:48+05:30
lastmod: 2020-03-30T04:17:48+05:30
draft: true
description: "This blog list down some of the terminal shortcuts to making your experience pleasant."
tags: []
keywords: []
categories: []
author: "Raman Tehlan"

images: ["https://user-images.githubusercontent.com/29037312/79038268-b27d9500-7bf5-11ea-980c-cea7ce97f179.jpg"]

---

<img src="https://user-images.githubusercontent.com/29037312/79038268-b27d9500-7bf5-11ea-980c-cea7ce97f179.jpg" width="745px" />

**Linux is probably the most powerful tool in the world**; When I used it for the first time, I instantly felt control over my system, and I started to understand the working of my computer with time. If you are reading this, and are not already using Linux, or haven't used it ever, I strongly recommend you try it out. In Linux, what I like the most is the **terminal, it's like magic**, it lets you reach the core of your system and work with it. I find it fast, flexible, and simple. This blog list down some of the terminal shortcuts to making your experience pleasant, I am confident it can also help you be more productive and effective.

> Note: Most essential or recommended shortcuts are in bold.

# Movement

- **`ctrl + a`: Move to the start of a line.**
- **`ctrl + e`: Move to the end of a line.**
- `ctrl + b`: Move back one character at a time.
- `alt + b`: Move back one word at a time.
- `ctrl + f`: Move forward one character at a time.
- `alt + f`: Move forward one word at a time.
- `ctrl + xx`: Move to the beginning of the line; change something and then press `ctrl + xx` again to come back to your initial position.

# Screen

- **`ctrl + l`: Clear the screen.**
- `ctrl + s`: Stop all output to the screen but not the process.
- `ctrl + q`: Resume output to the screen.

# Process

- **`ctrl + c`: Interrupt/Kill the current running process.**
- **`ctrl + z`: Suspend the current running process.**
- `ctrl + d`: Close the shell.

# Deleting

- **`ctrl + d`: Delete the character under the cursor.**
- `alt + d`: Delete the word after the cursor.
- `ctrl + h`: Delete the word before the cursor.

# History & Completion
- **`Tab`: Automatically complete the command.**
- **`ctrl + p` or `Up Arrow`: Fetch the previous command.**
- **`ctrl + n` or `Down Arrow`: Fetch the next command.**
- **`ctrl + r`: Start command history mode.**
- `alt + r`: Edit command fetched through `ctrl + r`.
- `ctrl + o`: Run a command you found with `ctrl + r`.
- `ctrl + g`: Exit history searching mode.

# Typos
- **`alt + t`: Swap the current word with the previous word.**
- `ctrl + t`: Swap the last two characters before the cursor with each other. 
- `ctrl + _`: Undo your last key press.

# Cuting & Pasting
- **`ctrl + w`: Cut the word before the cursor.**
- `ctrl + k`: Cut the line after the cursor.
- **`ctrl + u`: Cut the line.**
- **`ctrl + y`: Paste the last cut.**

# Capitalizing
- `alt + u`: Capitalize every character from the cursor to the end of the word.
- `alt + l`: Uncapitalize every character from the cursor to the end of the word
- `alt + c`: Capitalize the character under the cursor also moves cursor to the end of the word.

# Bang Bang (!)
- `!!`: Execute the last command.
- `!xyz`: Execute the recent command starting with `xyz`.
- `!$`: Execute the last word of the previous command.
- `!*`: Display the last word of the previous command.

use `:p` in the end of bang command to preview the command. Ex. `!$:p`

# Acknowledgement

- Header Photo by [Kristina Paparo](https://unsplash.com/@designshot) on [Unsplash](https://unsplash.com/photos/7p8R4CZjoQE)



> Let's discuss it on [Reddit](https://www.reddit.com/user/ramantehlan/comments/fvk3cg/terminal_shortcuts/) or [Twitter](https://twitter.com/ramantehlan/status/1246889936550113282)

