---
title: "Using Vim for a week!"
date: "2022-07-03"
description: &desc "Starting today, I have decided to be a masochist and use Vim for a week"
summary: *desc
tags: ["personal"]
---

I am writing this in Vim emulated VSCode because using Vim straight from the terminal
might make me dislike it and never look at it again, ThePrimeagen also recommended
emulating it in VSCode and so did the Learn Vim extension on VSCode marketplace.

The hardest part for me right now is the navigation, hjkl don't make a lot of sense and
my fingers try to go towards the arrow keys and I have to fight the urge to use
arrow keys 🗿.

Regardless, everything I do from today onwards shall be in VSCode emulated Vim.  
For some reason, my shortcuts do not work(like opening markdown preview using ctrl k v),
but I guess I'll have to live with that since I don't think that will be in Vim.  

I would also like to mention that by one week I mean 168 development hours in VSCode,
which includes writing this blog post. Because I could sleep for a week and tell the world
that I used Vim for a week and regretted it. I won't measure the time but hopefully my 
git history will be the evidence of what I did.

---

## Day 1

Today was incredibly tough and quite painful, though it really wasn't because of Vim
but because of VSCode messing up a few functions due to Vim emulation, again, can't really
blame either because it works as it should.

I would say that the Vim experience was rather good and made me feel quite
happy because I could actually feel the speed and I didn't use arrow keys as much!  
Although it is quite annoying to constantly switch between insert and normal mode, I think
I've gotten quite good at it.

Some of the major problems I faced were:  

1. Going to the end of the line to put a `;` in Rust.
2. Going to the beginning of the line.
3. Going to the position before `"` in a line like `println!("hello");`.
4. Copying and pasting, yanking feels ODD as HELL.
5. Duplicating a line.
6. Accidentally entering visual mode, how do I enter visual mode randomly? Perhaps `CTRL + V`?
7. Starting a new line.

Solutions to those major problems:  

1. `A;<ESC>`
2. `0`
3. `f";` - didn't bother finding another way
4. yanking and putting `yyp`
5. `yyp` again
6. No idea. Probably accidental.
7. o for a line below, O for a line above, {n}o/O for n lines above/below

Besides that, maybe I'll hang out in vimtutor for a bit.  

### Day 2

Nothing much besides learning a few more controls, getting the hang of vim bit by bit and
surprisingly, using those keybindings in places I shouldn't use, like Chrome or MS Word.  
New discoveries involve:  

1. `a` to enter insert mode in front of the character
2. `A` to enter insert mode at the last character in line
3. `I` to enter insert mode at the first character in line.
