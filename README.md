sublimetext2-customize-vintage-mode
===================================

Accompanying Sublime Text 2 configurations for my blog post on setting up Sublime in vintage mode.

# Customize key mapping and Vintage Mode setup for Sublime Text 2

If you're impatient, or you just want to use them as a reference my Sublime settings configurations have been made available at this [Github Repo](https://github.com/nackjicholson/sublimetext2-customize-vintage-mode)

---

### Why to switch from vim to Sublime Text 2 w/ Vintage Mode.

I really love vim, its the best text editor ever built. It allows you to do an almost unlimited amount of awesome things. And, you almost never have to remove your fingers from home row. Imagine how much time you lose messing around with your mouse and the arrow keys while you're coding. I'm not going to go into detail about why vim, and by association Vintage Mode, is going to revolutionize the way you code; I'll let Derek Wyatt do that. Watch his incredible video blog series [Vim Novice](http://www.derekwyatt.org/vim/vim-tutorial-videos/vim-novice-tutorial-videos/), if his fanaticism doesn't convince you to make the switch, just leave now, seriously go!

Okay, now that we've weeded out those folks I'll explain why even though vim is amazing, I decided to make the switch to Sublime. I honestly don't think Sublime is as powerful as vim, the thing about it is, vim is old as hell. It farts dust! I think its older than I am, and in tech time that's fucking Jurassic. In order to harness all that power you will have to get in your Delorian and become a super vim user, and with Sublime Text 2 -- it will just be easier. Sublime gives you an amazing editor out of the box, with all the conveniences of a modern 21st Century application, and enough of the "Vintage" power to keep you scorching code onto the screen. 

**Note: Everything below assumes you're using Mac OSX.**
If you're using Linux or Windows, you're probably smarter than me and don't need any help.

---

### Turn on Vintage Mode.

Sublime ships with Vintage mode installed, but ignored. Its pretty simple to turn on. Official instructions [here.](http://www.sublimetext.com/docs/2/vintage.html)

(Picture of Menu selection)

1. Preferences > Settings - Default
2. Search the file "ignored_packages".
3. Change this line.

        "ignored_packages": ["Vintage"]

      to:

        "ignored_packages": []

You're also going to need to add one little convenience to your User settings. Vintage Mode starts automatically starts in insert mode, and that's just stupid. When you're cruising around files you want to be in command mode so you can move around. Go back up to that menu and this time.

1. Preferences > Settings - User
2. Do this.

        {
          "vintage_start_in_command_mode": true
        }

Because sublime needs to initialize with the Vintage package for these changes to take effect you, should now quit sublime and restart it. When you open a file you should see the words "COMMAND MODE" in the lower left hand status bar. If you press `i` to enter "INSERT MODE" you should see that status change.

### How Sublime Key Mapping Works.

Did you notice your settings files are JSON objects? How much better is that than working with .vimrc? I told you this was going to be worth it. All of Sublimes settings are defined as JSON, including your newly initialized Vintage commands. If you're curious, all of the vim mappings are in this file `~/Library/Application Support/Sublime Text 2/Packages/Vintage/Default.sublime-keymap`.

Let's look at the first key map in that file:

    { "keys": ["escape"], "command": "exit_insert_mode",
      "context":
      [
        { "key": "setting.command_mode", "operand": false },
        { "key": "setting.is_widget", "operand": false }
      ]
    },    

The command is the `esc` key, which is traditionally the way you exit insert mode in vim. There are a few elements to this key mapping, we should take note of.

1. "keys": An array with a key combination that this mapping will respond to. In this case, the "escape" key.
2. "command": A method that sublime uses to do something.
3. "context": A configuration object that tells sublime to only respond to this key combination in the right context. In this case, `setting.command_mode` needs to be `false`. Meaning you're in insert mode. This makes sense, you can't exit insert mode, if you're not in it.

There are other components of key mapping I'm not going to go into, but for further explanation of this, and anything else Sublime related, go to the [Unofficial Documentation].

### Customizing Vintage Mode Key Mapping.

I prefer to enter insert by pressing `i` and exit it by pressing `ii` quickly in succession. The `escape` key is way over there in the middle of nowhere. Let's add another way to exit insert mode.

Open up your user key binding configuration file `Preferences > Key Bindings - User`. Copy that escape command we were looking at, but change the "keys" array like so.

    // vintage - mode control
    // exit insert mode
    { "keys": ["i", "i"], "command": "exit_insert_mode",
      "context":
      [
        { "key": "setting.command_mode", "operand": false },
        { "key": "setting.is_widget", "operand": false }
      ]
    },

This doesn't overwrite the default `escape` command, it just gives you an alternative way of doing the same thing. I suggest you look through my [Default (OSX).sublime-keymap]()