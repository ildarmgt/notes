# Important notes

## vscode

How to run run Sinatra/Ruby server from vscode with play button

* Get `Code Runner` extension
* Open settings: File > Preferences > settings or Ctrl + ,
* search for `code-runner.executorMap` setting
* hit pen icon to left of it to add it to custom settings
* change the key "ruby": to value (one-line):

``ruby $fileName || (echo;echo 'panic: ruby fail city';echo) & (sleep 1 && google-chrome http://localhost:4567/)&>/dev/null; (for i in `seq 1 10`;do echo;done); echo 'server up or fails here'; echo; fg&>/dev/null; echo;echo;echo 'server down'; echo; ps; echo 'make sure no ruby running ^ (fg and Ctrl-C otherwise)'; echo;``

* other settings:
```
"code-runner.runInTerminal": true,
"code-runner.saveFileBeforeRun": true,
"code-runner.saveAllFilesBeforeRun": true,
"code-runner.fileDirectoryAsCwd": true,
"code-runner.ignoreSelection": true,
"code-runner.showRunIconInEditorTitleMenu": true,
"code-runner.preserveFocus": false,
```
* now can right click app.rb and hit `run code` or use play button with app.rb open; when done, ctrl-c in terminal

it does:

1. run ruby file
2. wait 1 second
3. opens localhost:4567 in chrome (hide browser return outputs in terminal)
4. print 10 blank lines (so easier to see where server starts)
5. write `server up`
6. make sure server outputs are visible / at front
7. when terminated (e.g with Ctrl + C) say `server down`
8. show all running processes in that terminal to make sure no left over ruby server processes

