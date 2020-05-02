# thoughts

* For the two users to connect to each other - use plain IP address and port
number. See if the two users can connect to each other. If not, use something
like https://ngrok.com for now! 

* See if you can use gRPC client and server for the networking component. Easier
for code generation! We don't have to write too much client side code then -
connecting, serializing, deserializing data and all. And I think it's efficient
compared to HTTP, so 🤷‍♂

* Use golang for networking component!

* Write controller component code in Swift for now to move the mouse. Look
out for libraries and the https://github.com/BlueM/cliclick objective-c
code

* Check how to make the networking component and the controller component
talk to each other. More like inter process communication. We can do
gRPC again? In Swift code too. To start with. Let's see.

---

Assumptions: The relative position / movement of a mouse can be captured.

UI -> imagine a blank window program. If the user clicks on it, the mouse
disappears, but the program starts to capture the movement / position of the mouse.
And the movements are sent to the other user's computer. Now - are we sending
absolute position or relative position (movement) of the mouse?

If we are sending absolute position, it means the position from first user's
computer is taken up and the mouse is moved to exactly the same position
in the other user's computer. What are the pros and cons to that? If there are
resolution differences, then we will have to do a mapping of the screen and
accordingly change the position by scaling up or down and then controlling
the mouse. 

Assumptions: the mouse movement can and will be captured beyond the window's
limits.

If we are sending relative positions, more like movements, what's the speed
of the movement of the mouse? At OS level you can set how fast you want the
mouse to move. So, does that affect things here? 

Okay, it's clear that I don't know anything about mouses and the above is just
some random logic based thoughts. More like a layman thoughts. I need to do
some spikes to understand more about mouses! 

Spike 1: How does one capture the actions of a mouse and details of a mouse?
What's possible and what's not possible? Does one need a blank window to
capture a mouse? Can it be done with no windows? That is, no GUI, at all.
What are the limits to capturing the mouse's actions? When can we do it and
when can't we? As usual explore a lot to checkout the unknown unknowns.

Check [spike thoughts](./spikes/spike1/thoughts.md)
---

After the above spike, I have a lot of code already ready. Now, I'm just
trying to modify the electron app so that it can contact the swift server
and is able to move the mouse. Then I'll try it with my friend may be, over
the Internet

---

Currently trying to create a standalone nodejs client similar to the golang
client for the swift grpc server.

Trying out the code here

https://grpc.io/docs/tutorials/basic/node/#loading-service-descriptors-from-proto-files

When I installed stuff using `npm`, got some security issues. Can't have
security issues in my app 😅 so, checking it out. I did this

```
$ npm i -S grpc @grpc/proto-loader
```

Got errors regarding `minimist` package security vulnerability. And I tried
the automated fix

```
$ npm audit fix
npm WARN controller-demo-nodejs-client@0.1.0 No description
npm WARN controller-demo-nodejs-client@0.1.0 No repository field.

up to date in 0.514s
fixed 0 of 3 vulnerabilities in 172 scanned packages
  3 vulnerabilities required manual review and could not be updated
```

Manual review was needed.

```
$ npm audit

                       === npm audit security report ===

┌──────────────────────────────────────────────────────────────────────────────┐
│                                Manual Review                                 │
│            Some vulnerabilities require your attention to resolve            │
│                                                                              │
│         Visit https://go.npm.me/audit-guide for additional guidance          │
└──────────────────────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > mkdirp > minimist                      │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > tar > mkdirp > minimist                │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > rc > minimist                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
found 3 low severity vulnerabilities in 172 scanned packages
  3 vulnerabilities require manual review. See the full report for details.
```

So, now I checked all these links

https://www.npmjs.com/advisories/1179

https://github.com/substack/minimist/commit/4cf1354839cb972e38496d35e12f806eea92c11f#diff-a1e0ee62c91705696ddb71aa30ad4f95
https://github.com/substack/minimist/commit/63e7ed05aa4b1889ec2f3b196426db4500cbda94

I need to understand the security vulnerability, for now trying to get rid of it

https://github.com/substack/minimist/commit/4cf1354839cb972e38496d35e12f806eea92c11f#commitcomment-38002136

https://github.com/maxogden/extract-zip/issues/86#issuecomment-602133618

https://www.npmjs.com/package/npm-force-resolutions

https://stackoverflow.com/a/60795003/1611925 or
https://stackoverflow.com/questions/58065817/npm-force-package-lock-to-update-a-sub-dependency-package/60795003#60795003

https://stackoverflow.com/a/60794976/1611925 or
https://stackoverflow.com/questions/53262690/force-npm-to-update-dependency/60794976#60794976

```
$ npm ls minimist
controller-demo-nodejs-client@0.1.0 /Users/karuppiahn/oss/github.com/karuppiah7890/controller-demo-nodejs-client
└─┬ grpc@1.24.2
  └─┬ node-pre-gyp@0.14.0
    ├─┬ mkdirp@0.5.1
    │ └── minimist@0.0.8
    └─┬ rc@1.2.8
      └── minimist@1.2.0
```

I'm just going to force everything to use `minimist@1.2.5` which is the latest

https://github.com/substack/minimist/releases

Hopefully no breaking changes 🤔 as `mkdirp@0.5.1` is using `0.0.8` version of `minimist`.
Let me check if they have actually upgraded. Okay, the latest version of
`mkdirp` is `1.0.4` https://www.npmjs.com/package/mkdirp?activeTab=versions , https://github.com/isaacs/node-mkdirp/releases

Actually, I could just lock the version for `mkdirp` and `rc`. Hmm 🤔

Wow. So, I tried different stuff. In between I realized `resolutions` is a
feature provided by `yarn` package manager 

https://classic.yarnpkg.com/en/docs/selective-version-resolutions/

Finally, I just got rid of `package-lock.json` and added it to `.gitignore`
and started using `yarn`. Surprsingly no audit issues this time. No vulnerabilities.
I got rid of the `resolutions` field in my `package.json` too!

Back to coding! Damn :P Spent too much time on that security issue.

Now, I'm trying to see how to load multiple proto files. In the code I see
this

```
/**
 * Load a .proto file with the specified options.
 * @param filename One or multiple file paths to load. Can be an absolute path
 *     or relative to an include path.
 * @param options.keepCase Preserve field names. The default is to change them
 *     to camel case.
 * @param options.longs The type that should be used to represent `long` values.
 *     Valid options are `Number` and `String`. Defaults to a `Long` object type
 *     from a library.
 * @param options.enums The type that should be used to represent `enum` values.
 *     The only valid option is `String`. Defaults to the numeric value.
 * @param options.bytes The type that should be used to represent `bytes`
 *     values. Valid options are `Array` and `String`. The default is to use
 *     `Buffer`.
 * @param options.defaults Set default values on output objects. Defaults to
 *     `false`.
 * @param options.arrays Set empty arrays for missing array values even if
 *     `defaults` is `false`. Defaults to `false`.
 * @param options.objects Set empty objects for missing object values even if
 *     `defaults` is `false`. Defaults to `false`.
 * @param options.oneofs Set virtual oneof properties to the present field's
 *     name
 * @param options.includeDirs Paths to search for imported `.proto` files.
 */
export declare function load(filename: string | string[], options?: Options): Promise<PackageDefinition>;
export declare function loadSync(filename: string | string[], options?: Options): PackageDefinition;
```

Not sure how to pass multiple file paths in a single string. 🤔But there's this
option called `includeDirs`. I could use that so that imports don't have
problems. Okay then. There's a way to load proto files with `import` statements

From the swift repo, I had to copy proto files

```
$  cp controller-demo/protos/*proto ../controller-demo-nodejs-client/protos/
```

I gotta see how to have it in a central place and keep it updated too 🤔 Hmm.
Not sure if mono repos can help. Quite possible :D Let's see. For now, copy
paste is fine. I guess 🙈

I used this to understand the keys inside the object

```
 console.log(Object.keys(protoDescriptor))
```

Wow. I was able to write the code and connect to it and move the mouse too
by contacting the swift grpc server!!! :D :D :D 

Now, I had to copy paste code from the nodejs client to my remote-ui app
(eletron app) and I replaced package-lock.json with yarn.lock over there
too. Now, with all the code inside, I'm seeing if anything works, but the
console is giving me this error

```
Uncaught Error: Failed to load gRPC binary module because it was not installed for the current system
Expected directory: electron-v8.2-darwin-x64-unknown
Found: [node-v72-darwin-x64-unknown]
This problem can often be fixed by running "npm rebuild" on the current system
Original error: Cannot find module '/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node'
Require stack:
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/grpc_extension.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/client_interceptors.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/client.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/index.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/index.html
    at Object.<anonymous> (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/grpc_extension.js:53)
    at Object.<anonymous> (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/grpc_extension.js:64)
    at Module._compile (internal/modules/cjs/loader.js:968)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:986)
    at Module.load (internal/modules/cjs/loader.js:816)
    at Module._load (internal/modules/cjs/loader.js:728)
    at Module._load (electron/js2c/asar.js:717)
    at Function.Module._load (electron/js2c/asar.js:717)
    at Module.require (internal/modules/cjs/loader.js:853)
    at require (internal/modules/cjs/helpers.js:74)
```

Gotta work on it and fix it! :) And then I'll be good to try it out over the
Internet. Hopefully in the mean time no one will hack things. But I can
see my mouse movements, so let's hope I can find out just in case anyone
messed with my system while doing the trial with my friends

Okay, after reading some links

https://duckduckgo.com/?q=expected+electron-v8.2-darwin-x64-unknown+Found%3A+%5Bnode-v72-darwin-x64-unknown%5D&t=ffab&ia=web
https://github.com/nodejs/node-gyp/issues/1599
https://github.com/grpc/grpc-node/issues/594
https://docs.npmjs.com/cli/rebuild
https://duckduckgo.com/?t=ffab&q=npm+rebuild+for+electron&ia=web
https://www.npmjs.com/package/electron-rebuild
https://www.electronjs.org/docs/tutorial/using-native-node-modules
https://duckduckgo.com/?t=ffab&q=Expected+directory%3A+electron-v8.2-darwin-x64-unknown
https://stackoverflow.com/questions/55144432/how-do-i-install-grpc-for-electron-version-4-0-x
https://duckduckgo.com/?t=ffab&q=grpc+in+electron&ia=web
https://stackoverflow.com/questions/40265877/using-grpc-in-electron

I finally was able to get rid of the above error by doing this

```
$ ls node_modules/grpc/src/node/extension_binary/node-v72-darwin-x64-unknown/grpc_node.node
$ # the above is what is present.
$ # but no electron directory is present. which is
$ # what my electron app is looking for.
$ # so I did this
$ yarn add -D electron-rebuild
$ npx electron-rebuild
$ ls node_modules/grpc/src/node/extension_binary/
$ ls node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node
```

So, that error is gone. Now I have a new error. Lol 😂

```
Uncaught TypeError: Cannot read property 'readFileSync' of null
    at fetch (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/node_modules/protobufjs/src/root.js:162)
    at Root.load (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/node_modules/protobufjs/src/root.js:196)
    at Root.loadSync (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/node_modules/protobufjs/src/root.js:237)
    at Object.loadSync (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/node_modules/protobufjs/src/index-light.js:69)
    at Object.<anonymous> (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/build/src/index.js:230)
    at Object.<anonymous> (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/build/src/index.js:235)
    at Module._compile (internal/modules/cjs/loader.js:968)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:986)
    at Module.load (internal/modules/cjs/loader.js:816)
    at Module._load (internal/modules/cjs/loader.js:728)

---

DevTools failed to parse SourceMap: file:///Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/@grpc/proto-loader/build/src/index.js.map
```

Now, I gotta see what's wrong here. For now I can see that the proto file paths
are good, using `console.log()`s

Saw these links

https://github.com/protobufjs/protobuf.js/blob/4ecfbcedaa4a9a85b9e896f38608519643390db4/src/root.js#L162
https://github.com/protobufjs/protobuf.js/blob/4ecfbcedaa4a9a85b9e896f38608519643390db4/src/util.js#L22
https://duckduckgo.com/?t=ffab&q=fs+in+electron&ia=web
https://stackoverflow.com/questions/37994441/how-to-use-fs-module-inside-electron-atom-webpack-application#38021584


Okay, I think may be the issue is that - the `fs` module is not available
to the js code. I moved the code to the main process `index.js` and it worked!
Initially the code was being run inside the windows's JS file. Not sure if the
electron rebuild thing is still needed. Need to check that out! 

To check that, I did this

```
$ mv node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node.bak
```

and then ran and got these errors in a error window and in the console too

```
Uncaught Exception:
Error: Failed to load /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node. Cannot find module '/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node'
Require stack:
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/grpc_extension.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/client_interceptors.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/client.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/index.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/index.js
- /Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/electron/dist/Electron.app/Contents/Resources/default_app.asar/main.js
- 
    at Module._resolveFilename (internal/modules/cjs/loader.js:798:15)
    at Function../lib/common/reset-search-paths.ts.Module._resolveFilename (electron/js2c/browser_init.js:7620:16)
    at Module._load (internal/modules/cjs/loader.js:691:27)
    at Module._load (electron/js2c/asar.js:717:26)
    at Function.Module._load (electron/js2c/asar.js:717:26)
    at Module.require (internal/modules/cjs/loader.js:853:19)
    at require (internal/modules/cjs/helpers.js:74:18)
    at Object.<anonymous> (/Users/karuppiahn/oss/github.com/karuppiah7890/remote-ui-app-demo/node_modules/grpc/src/grpc_extension.js:32:13)
    at Module._compile (internal/modules/cjs/loader.js:968:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:986:10)
```

So, reverting my change! 

```
$ mv node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node.bak node_modules/grpc/src/node/extension_binary/electron-v8.2-darwin-x64-unknown/grpc_node.node
```

So, now, to make the whole thing work, I was thinking if I should just send
the mouse point information from the browser js file to the main process
and then from there send it to the grpc server!

https://www.electronjs.org/docs/api/ipc-renderer#ipcrenderersendchannel-args
https://www.electronjs.org/docs/api/ipc-main#ipcmainonchannel-listener

https://www.electronjs.org/docs/api/ipc-main#sending-messages

It's all asynchronous it seems. The only weird thing would be - if all the
messages go out of order, it's gonna be a bit messed up :P

Apparently there's an sync version for renderer - https://www.electronjs.org/docs/api/ipc-renderer#ipcrenderersendsyncchannel-args

But it's warned that the renderer process will block. Of course. It's synchronous.

Let's see how the async one goes ;) :D :)

Okay, so I made the communication work! I logged the mouse point information
in the main process

```
...
{ sX: 578, sY: 322, sDx: 578, sDy: 322 }
{ sX: 578, sY: 322, sDx: 0, sDy: 0 }
{ sX: 579, sY: 322, sDx: 1, sDy: 0 }
{ sX: 592, sY: 319, sDx: 13, sDy: -3 }
{ sX: 605, sY: 318, sDx: 13, sDy: -1 }
{ sX: 612, sY: 317, sDx: 7, sDy: -1 }
{ sX: 615, sY: 317, sDx: 3, sDy: 0 }
{ sX: 616, sY: 317, sDx: 1, sDy: 0 }
...
```

I just didn't communicate the same with server, because, well, you know, it's
like, my mouse, controlling itself o.O Let me try it though. It's gonna be weird!

I got some really weird behavior. Of course. Also, given the fact that the
server does not move the cursor based on absolute coordinates, and instead moves
it based on relative positioning! :)

Now I want to try it with my friend. I need to package it and send it to her.
I found out how to package 

https://www.electronjs.org/docs/tutorial/application-packaging
https://github.com/electron/electron-packager
https://github.com/electron/electron-packager/blob/master/usage.txt

```
$ yarn add -D electron-packager
$ npx electron-packager -h
$ npx electron-packager . remote-ui
$ ls remote-ui-darwin-x64/remote-ui.app/
```

I was able to open the app and all. Now, the only thing remaining is - making
the input for server url and port straight forward. I think I'll put a
text box and connect button in the browser and get the input :)

Okay, I was able to put a text box and get input and connect to the grpc
server after the click of the "connect" button

I then tested it with my friend. This is what I did for the setup

1. Started the controller server (swift code. grpc server). The port was some
random port
2. Started ngrok
```
$ ngrok tcp <port>
```
3. Got the ngrok URL with port, and gave it to my friend
4. I also gave the remote ui app (electron app) in a zip file to her, through
my google drive
5. She opened the app, allowed it in her security preferences and then allow
my app
6. She typed in the url and port in the input and connected and boom, she was
able to control my mouse

Since the app does not do screen sharing, I was showing her my screen through
hangouts and she could see how the movement of the mouse was. This was the
feedback that we came up with

1. It was laggy. I mean, this was kinda obvious, because when I was trying it
in my local, the connectivity is of course fast, later when I tried from my
local to local server through ngrok just to check if ngrok connectivity works,
I realized there was some lag, for even one mouse point move. Also, I think the
fact that I do multiple method calls vs streaming input could also be a thing.
And then, another thing is - Internet, along with ngrok being the middle thing,
and she was seeing the mouse move through Hangouts meet, so, that's weird, I
mean, Hangouts meet could be showing the screen a bit later, with some lag,
so yeah, that could bring in some false sense of lag too. Anyways. So, that
was that
2. Not able to move much. So, this came from the fact that, currently the remote
ui app just captures mouse movement when the mouse is within the app window,
and the mouse control is based on relative positioning and moving. So, when my
friend moved the mouse a lot, she could not as she moved out of the app window
and lost control after that. Later this got me thinking. How do I make this
better then? So, absolution might be crazy - because if the remote ui app
window is small, a small movement there will be a big movement here. But it will
make sure that there's freedom to move and all. But ideally, come to think of it,
let's say I move my mouse to the end of the app window, to the corner and the
app window is in full screen mode or just fitting the whole screen, and on the
other side, based on relative positioning, the mouse moved, but is still somewhere
in the middle of the screen, that's weird right? because of the problems
relative position brings in. Instead, what if I never relied on mouse position?
And instead just relied on the input from the trackpad? Not sure if it's possible,
but that's what is the main source of input right? I move a bit in it, and the
mouse moves, just that, in this case, the local mouse moves and based on that
another remote mouse moves. Instead, why not move the remote mouse based on the
trackpad and forget about the local mouse - it does not matter where the local
mouse is - we can just hide it, and also allow movement outside the app window,
but the mouse control happens only when app window is focused, so that you can
get back your cursor in case you wanna do something else. I don't know. This
could be a possible thing. This could bring possible problems for the user if they want
to get back their control to the local mouse and also see the local mouse. There
must be some way to lose control of the remote mouse. Gotta see what to do.
Currently they can just do "Command + Tab" and they can switch apps and cursor
will be visible, but later when keyboard control also comes into place, that's
not a viable solution to bring back the cursor from it's hidden mode and also
be able to control it. Hmm. 

Gotta see if the above ideas make sense and then work on them after coming to
a conclusion on what's the idea to control the mouse. That would be MVP 2 I
think.

