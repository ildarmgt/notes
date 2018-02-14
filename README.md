# Important notes #

## vscode ##

### How to run Sinatra/Ruby server & open it in chrome instantly from vscode ###

**Result**: to test a build, only have to right click controller (e.g. app.rb), click `run code`, should open localhost in browser ~ 1 second later with server up. (Play button on rb file also works.) Ctrl-C to get out

* Get `Code Runner` extension
* Open vscode settings: File > Preferences > settings or Ctrl + ,
* search for `code-runner.executorMap` setting
* hit pen icon to left of it to add it to custom settings
* change the key "ruby": to value (one-line):

``
  ruby $fileName || (echo;echo 'panic: ruby fail city';echo) & (sleep 1 && google-chrome http://localhost:4567/ --incognito)&>/dev/null; (for i in `seq 1 10`;do echo;done); echo 'server up or fails here'; echo; fg&>/dev/null; echo;echo;echo 'server down'; echo; ps; echo 'make sure no ruby running ^ (fg and Ctrl-C otherwise)'; echo;
``

  * Changing how to launch chrome:
    * Linux/Ubutu: `google-chrome http://localhost:4567/ --incognito`
    * OSX `open -a /Applications/Google Chrome.app --args --incognito` (not verified)
    * remove --incognito to launch in default browser session
    * could use directly in terminal, but need to replace $filename with ruby controller file necessary like app.rb

* Other vscode core-runner settings:
```
  "code-runner.runInTerminal": true,
  "code-runner.saveFileBeforeRun": true,
  "code-runner.saveAllFilesBeforeRun": true,
  "code-runner.fileDirectoryAsCwd": true,
  "code-runner.ignoreSelection": true,
  "code-runner.showRunIconInEditorTitleMenu": true,
  "code-runner.preserveFocus": false,
```

**Done**

what plug-in does:

  * with those settings, sends the long terminal command to internal terminal

what terminal command does:

  1. run selected ruby file
  2. wait 1 second
  3. opens localhost:4567 in chrome (hide browser return outputs in terminal)
  4. print 10 blank lines (so easier to see where server starts)
  5. write `server up`
  6. make sure server outputs are visible / at front
  7. if ruby process returns error, say `ruby fail` (shouldn't say it if terminated by Ctrl-C)
  8. when ruby process terminated, say `server down`
  9. show all running processes in that terminal to make sure no left over ruby server processes

