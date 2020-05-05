I'm going to show the explorer with dummy data. Going to check this
out

https://github.com/Microsoft/vscode-extension-samples/tree/master/fsprovider-sample
https://code.visualstudio.com/api/references/vscode-api#workspace.registerFileSystemProvider

So, I'm currently running the sample extension. It's really cool. I'm able to
setup a memory based file system from the command palette. And only after
creating the file system, I can see more options in the command palette related
to the extension, like to create files and more

I tried creating a golang file. On activating the golang extension for the
workspace, the extension gave errors saying the uri scheme is not supported
and that `gopls` supports only file uris. Makes sense

This looks really cool! Deleting files, creating files and what not! :) :D

I need to now see how to create a dummy file system provider :P

