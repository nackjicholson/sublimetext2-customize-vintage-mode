sublimetext2-customize-vintage-mode
===================================

> Accompanying Sublime Text 2 configurations for my blog post on setting up Sublime in vintage mode.

[The Blog](http://projectpoppycock.com/key-mapping-and-vintage-mode-setup-for-sublime-text-2)

# Customize key mapping and Vintage Mode setup for Sublime Text 2

If you're impatient or just want a reference, my Sublime configurations have been made available at this [Github Repo][1]

* * * 

### Why switch from vim to Sublime Text 2 and Vintage Mode.

First of all, I love vim, its the best text editor ever built. It allows you to do an almost unlimited amount of awesome things. And you almost never have to remove your fingers from home row. Imagine how much time you lose messing with the mouse and arrow keys while you're coding. I'm not going to go into detail about why vim key mapping, is going to revolutionize the way you code; I'll let Derek Wyatt do that. Watch his incredible video blog series [Vim Novice][2]. If his excitement and fanaticism doesn't convince you to make the switch, just leave now, you're not going to "Get It". Seriously. Go!

Now that we've weeded out those chumps, I'll explain why even though vim is amazing, I decided to make the switch to Sublime. I honestly don't think Sublime is as powerful as vim, but the thing about it is, vim is old as hell. It farts dust! I think its older than I am, and in tech time that's fucking Jurassic. In order to harness all that power you will have to get in your DeLorean and become a vim superuser, and with Sublime Text 2 -- you won't. Sublime gives you an amazing editor out of the box, with all the conveniences of a modern 21st Century application, and enough of the "Vintage" power to keep you scorching code onto the screen.

**Note: Everything below assumes you're using Mac OSX.** If you're using Linux or Windows, you're probably smarter than me and don't need any help.

* * *

### Turn on Vintage Mode.

Sublime ships with Vintage mode installed, but ignored. Its pretty simple to turn on. Official instructions [here.][3]

[<img src="http://projectpoppycock.com/wp-content/uploads/2013/04/Screen-Shot-2013-04-25-at-12.24.06-PM.png" alt="Screen Shot 2013-04-25 at 12.24.06 PM" width="600" height="300" class="alignleft size-full wp-image-487" />][4]

1.  `Preferences > Settings - Default`
2.  Search the file "ignored_packages".
3.  Change this line.
    
        "ignored_packages": ["Vintage"]
        
    
    to:
    
        "ignored_packages": []
        

You're also going to need to add one little convenience to your User settings. Vintage Mode automatically starts in insert mode, and that's just stupid. When you're cruising around files you want to be in command mode so you can move around. Go back up to that menu.

1.  `Preferences > Settings - User`
2.  Do this.
    
        {
          "vintage_start_in_command_mode": true
        }
        

Because sublime needs to initialize with the Vintage package for these changes to take effect, you should now quit and restart. When you open a file you should see the words "COMMAND MODE" in the lower left hand status bar. If you press `i` to enter "INSERT MODE" you should see that status change.

### How Sublime Key Mapping Works.

Did you notice your config files are JSON objects? How much better is that than working with .vimrc? I told you this was going to be worth it! All of Sublimes' settings are defined as JSON, including your Vintage commands. If you're curious, all of the Vintage mappings are in this file `~/Library/Application Support/Sublime Text 2/Packages/Vintage/Default.sublime-keymap`.

Let's look at the first key map in that file:

    { "keys": ["escape"], "command": "exit_insert_mode",
      "context":
      [
        { "key": "setting.command_mode", "operand": false },
        { "key": "setting.is_widget", "operand": false }
      ]
    },    
    

The command is the `esc` key, which is traditionally the way you exit insert mode in vim. There are a few elements to this key mapping, we should take note of.

1.  "keys": An array with a key combination that this mapping will respond to. In this case, the "escape" key.
2.  "command": A method that sublime uses internally to accomplish the task.
3.  "context": A configuration object that tells sublime to only respond to this key combination under specific circumstances. In this case, `setting.command_mode` needs to be `false`. Meaning you're in insert mode. This makes sense, you can't exit insert mode, if you're not in it.

There are other components of key mapping I'm not going to go into, but for further explanation of this, and anything else Sublime related, go to the [Unofficial Documentation][5].

### Customizing Vintage Mode Key Mappings.

I prefer to enter insert by pressing `i` and exit it by pressing `ii` in quick succession. The `escape` key is way over there in the middle of nowhere, I DO NOT WANT TO LEAVE HOME ROW! Let's add another way to exit insert mode.

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
    

This doesn't overwrite the default `escape` command, it just gives you an alternative way of doing the same thing.

### Use my files

If you'd like to use the same setup I do, I encourage you to take my config files from the [Github Repo][1] and use their contents in your own.

Some of the things they give you:

*   `super+.` Opens up the Key Bindings - User file, so you don't have to dig through the menu.
*   `,cc` Close file
*   `,vs` Vertically split my Sublime Window.
*   `,l` Move to the right window
*   `,ml` Move a file to the right window.
*   etc.

FYI the `,` key is a good choice as a "leader" in key combinations because it has no command of its own.

### Share your mappings with me!

If you figure out a dope way to do something, submit a pull request to my [repo][1]. I can't promise I'll accept it, but if I think what you did is useful I will most definitely integrate it in. Cheers, go back to coding, thanks for reading.

 [1]: https://github.com/nackjicholson/sublimetext2-customize-vintage-mode
 [2]: http://www.derekwyatt.org/vim/vim-tutorial-videos/vim-novice-tutorial-videos/
 [3]: http://www.sublimetext.com/docs/2/vintage.html
 [4]: http://projectpoppycock.com/wp-content/uploads/2013/04/Screen-Shot-2013-04-25-at-12.24.06-PM.png
 [5]: http://docs.sublimetext.info/en/latest/customization/key_bindings.html