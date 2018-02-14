# Important notes

## vscode

How to run run Sinatra/Ruby server from vscode with play button

* Get `Code Runner` extension
* Open settings: File > Preferences > settings or Ctrl + ,
* search for `code-runner.executorMap` setting
* hit pen icon to left of it to add it to custom settings
* change the key "ruby": to value (one-line):

``ruby $fileName || (echo 'ruby panic fail city'; exit 0) & (sleep 1 && google-chrome http://localhost:4567/)&>/dev/null; (for i in `seq 1 10`;do echo;done); echo 'server up'; fg&>/dev/null; ps; echo 'make sure no ruby process ^ - server rekt'``

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
* now can right click app.rb or w/e, hit `run code`, when done, ctrl-c in terminal

it does:

1. run ruby file
2. if fails, write something
3. otherwise wait 1 sec
4. open it in browser (hide errors)
5. print 10 blank lines
6. write `server up`
7. make sure server outputs are visible
8. when terminated with Ctrl + C, show all running processes in that terminal

