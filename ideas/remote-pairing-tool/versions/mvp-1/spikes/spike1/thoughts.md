Spike 1: How does one capture the actions of a mouse and details of a mouse?
What's possible and what's not possible? Does one need a blank window to
capture a mouse? Can it be done with no windows? That is, no GUI, at all.
What are the limits to capturing the mouse's actions? When can we do it and
when can't we? As usual explore a lot to checkout the unknown unknowns.

---

Goals:
1. Track mouse inside the app
2. Track movement only when there's movement - do not poll please!
3. Track absolute position and the difference between previous position
and current position. More like dx and dy in math
4. Check what is possible

---

Okay, so I've started with checking about how to capture the mouse "stuff"

I remember seeing this thing called "Core Graphics"

https://developer.apple.com/documentation/coregraphics

It includes services for working with low level user input events. Which
lead me to this

https://developer.apple.com/documentation/coregraphics/quartz_event_services

I need to learn what features this thing provides and how to use it to my own
advantage for my goal of capturing mouse "stuff"

Okay, I read something about tapping events. I don't think I need to tap into
mouse events and change it or something. Let's see. For now I can see some
mouse related stuff in the docs of quartz event services.

I have created a new project - mouse-capture-cli . Yes, I'm trying it out
in a CLI app to check if it can be done completely in the background! :)

I used XCode to create the project. I'm using Swift. It asked Deployment
Target and I chose version `10.6` as that was the smallest and I wanted
to support as much as possible. Let's see what features I can get with that.

And the project document is in verison `9.3` X Code format I think. I was planning
to use version `11.4` which is the version of X Code I'm using but then I didn't
care.

I built the hello world program and it failed. The error says

```
Swift requires a minimum deployment target of OS X 10.9
```

So, let's choose that! I think that was what the already chosen version was,
and I went and changed it :P 🙈

So, my hello world works now. I even removed the line of code that
said `import Foundation` and it still worked. So, all cool! :P :D

Now, let's do some mouse stuff. Now, can I get where my mouse is present?
It's position?

Okay, I tried quite some stuff. I'm still stuck actually. The idea was to
use this 

https://developer.apple.com/documentation/coregraphics/cgevent/1455788-location

For which this was needed

https://developer.apple.com/documentation/coregraphics/cgevent

But I couldn't create an instance of `CGEvent` and I messed up completely
with Swift code. Lol. Too many errors 🙈I did find out that I need to
`import CoreGraphics` to do `CGEvent` stuff

I need to learn it. I think I'll learn it a bit on the go? I guess. And since
I couldn't get it to work, I started checking the docs which I saw about
moving a cursor. It's this one 

https://developer.apple.com/documentation/coregraphics/1455258-cgdisplaymovecursortopoint

So, I tracked back from there to this place

https://developer.apple.com/documentation/coregraphics/quartz_display_services
https://developer.apple.com/documentation/coregraphics/quartz_display_services#1656828

There's a section called `Controlling the Mouse Cursor` here! And there's this
thing called `CGGetLastMouseDelta()`

https://developer.apple.com/documentation/coregraphics/2437197-cggetlastmousedelta

Gotta check how that helps. Also, in this page, they recommend checking `NSEvent`
class for tracking mouse

https://developer.apple.com/documentation/appkit/nsevent 

I think I'll be checking this out

https://developer.apple.com/documentation/appkit/nsevent/1532495-mouseevent

Let's see how that goes!

I also checked this

https://duckduckgo.com/?q=obtain+mouse+location+in+macos&t=ffab&ia=web

Okay, so

https://developer.apple.com/documentation/appkit/nsevent/1532495-mouseevent

looks like creation of a mouse event. I think we need to "capture events" and
not create them. So, I saw this thing -

https://developer.apple.com/documentation/appkit/nsevent#1652040

Looks like the events are captured at our app window level or global level. I think
we should do our app window level - I mean, we should capture mouse events only in our
program and then use them to control the other user's program. This way, when
the user is focussed on another application, they can still focus on it,
without disrupting the other user's computer by controlling their screen,
and that's totally not intuitive and looks crazy and surely it will be
unintentional controlling by the user. 

So, seems like we do need an application with some GUI. Hmm. Let's still try
to use some code here and see if it works as a CLI application. Hmm

https://developer.apple.com/documentation/appkit/nsevent/1534971-addlocalmonitorforevents

So, I saw this answer

https://stackoverflow.com/questions/31931403/getting-mouse-coordinates-in-swift#31932049

I noticed one thing. In all the docs - I was looking at AppKit. Apparently it's
an old thing. Later came UI Kit I think? And the latest is Swift UI? But I can't
seem to find if there's any new way to do things - to capture mouse events,
other than the methods and functionality present in AppKit's NSEvent stuff.

I tried to then put the AppKit code in Swift UI by checking this

https://developer.apple.com/documentation/swiftui#3126401

`User Interface` > `Framework Integration` section

https://developer.apple.com/documentation/swiftui/framework_integration

https://developer.apple.com/documentation/swiftui/framework_integration#3126390

https://developer.apple.com/documentation/swiftui/nsviewcontrollerrepresentable

I also looked at these links

https://duckduckgo.com/?t=ffab&q=mouse+events+with+swift+ui+in+mac&ia=web

https://duckduckgo.com/?t=ffab&q=appkit+vs+swift+ui&ia=web

https://duckduckgo.com/?t=ffab&q=swift+protocols&ia=web

https://docs.swift.org/swift-book/LanguageGuide/Protocols.html (protocol
seems like interfaces in golang)

I tried too hard, but it didn't work out. I still got tons to learn first. So,
yeah. 

I need to start understanding how these things work one by one - may be
just enough - to make this work! So that I can understand what's possible
at least a bit. It just looks like - as usual I'm beating around the bush.
Need to learn some basics for the code I have read till now.


--

OH MY GOD. Okay. So, according to my architecture, this whole thing is part
of the Remote UI, which is responsible for capturing the mouse and keyboard
events! DAMN! I completely forgot about it 🙈 I mean, this is important
information because - I was planning to create a cross platform Remote GUI.
In the above solution - I was making more of a OS specific solution. So, yeah.
May be the next thing to do is - for now, stick to cross platform! :D :) 
So, I think I'll try ElectronJS framework. I remember checking out about it's
mouse event docs. I checked it out again now. This is the one

https://www.electronjs.org/docs
https://www.electronjs.org/docs/api/structures/mouse-input-event
https://www.electronjs.org/docs/api/structures/mouse-wheel-input-event

And it also has keyboard events stuff for the future -

https://www.electronjs.org/docs/tutorial/keyboard-shortcuts
https://www.electronjs.org/docs/api/structures/keyboard-event
https://www.electronjs.org/docs/api/structures/keyboard-input-event

Damn it. I can't believe I spent so much time on the above. I do have to learn
Swift though. For the controller part. And it would be nice to know how to
listen to inputs too. And see what magic I can do with Swift code, compared to
ElectronJS and others. For now I'll stick to ElectronJS and make it work first!

---

ElectronJS is really really cool! I just saw some demos of it's really cool
features using a demo app of theirs

https://github.com/electron/electron-api-demos/releases

And I also tried a quick quick-start thing :P

```
# Clone the Quick Start repository
$ git clone https://github.com/electron/electron-quick-start

# Go into the repository
$ cd electron-quick-start

# Install the dependencies and run
$ npm install && npm start
```

I think this is going to be awesome! :D ;) 

---

Okay, I was trying to capture the mouse movement and it's position. I realized
that the docs  I saw for mouse and keyboard events - they were type definitions
🤦‍♂ and there was not any API to get that event. Instead there's one API to
send event

https://www.electronjs.org/docs/api/web-contents#contentssendinputeventinputevent
https://www.electronjs.org/docs/api/webview-tag#webviewsendinputeventevent

And then I saw some libraries related to mouse (just saw readme)

https://github.com/gamedev-js/input.js
https://github.com/eshkol/dragula
https://github.com/wilix-team/iohook
https://github.com/rpa-helpers/iohook-lib
https://github.com/kapetan/electron-drag
https://github.com/kapetan/osx-mouse

I tried https://github.com/kapetan/osx-mouse and it looks really cool! It's able to track
the mouse in the whole screen! But it's specific to OS X. Hmm. I think it's okay
for now? To start with that is. We can check cross platform later

I also checked some more npm packages. Seems like there are react based
modules! For tracking mouse! Since I'm implementing with Electron which has
web technologies - I could use that. Also, I want to track only inside the app.

I checked some links

https://www.npmjs.com/package/react-hook-mighty-mouse
demo - https://mkosir.github.io/react-hook-mighty-mouse/?path=/story/react-mighty-mouse--flashlight

that was really nice. Some more are below

https://www.npmjs.com/package/@react-hook/mouse-position

I went off track and saw some more cool stuff

https://www.npmjs.com/package/proximity-effect
http://adasha.com/lab/proximity-effect/
http://adasha.com/lab/proximity-effect/1.html
http://adasha.com/lab/proximity-effect/2.html
http://adasha.com/lab/proximity-effect/3.html
http://adasha.com/lab/proximity-effect/4.html
http://adasha.com/lab/proximity-effect/5.html
http://adasha.com/lab/proximity-effect/6.html

Saw some more links 

https://www.w3schools.com/jsref/event_onmousemove.asp
https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_onmousemove

https://www.w3schools.com/jsref/event_clientx.asp
https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_event_mouse_screenxy_clientxy

https://www.w3schools.com/jsref/dom_obj_event.asp

---


So I finally did changes to the code to find the absolute position and the
difference in x,y coordinates too. In between I had to check how to make
the height and width of the body match the browser height and width

https://duckduckgo.com/?t=ffab&q=change+body+width+to+match+browser

https://stackoverflow.com/questions/1575141/how-to-make-a-div-100-height-of-the-browser-window?page=1&tab=votes#tab-top

I finally used `100vh` for `height` and `100vw` for `width` and also had to
put `margin` as `0` as there was some default `margin` of `8px` or something

---

Okay, so I was able to get the current location of the mouse in swift and was
also able to move the mouse! :D Current location was needed so that I can move
it to the correct absolute position by adding the dx and dy to the current
location, so it's like

(x, y) initially and then (x + dx, y + dy)

where we get dx and dy through grpc. Currently I'm planning to put in the
grpc, the networking component, along with controller or the remote UI. Not yet
doing separate components. I want to see how this goes and later think on the
pros and cons of each. I mean, if it's a separate program - that will be more
like a proxy in front of the remote UI or controller. And I also need to see
how to do inter process communication between two processes in the same machine.
To avoid that hassle - planning to join the features for now. Let's see how
that goes :P

So, I need to create a grpc server in swift and a grpc client in js. Then
the js in electron will send dx, dy data to swift grpc server and then the
server will do the controller stuff ;) This is gonna be cool I guess :P :D

---

Okay, so, I tried to write a proto and do stuff. The links I followed are

https://github.com/apple/swift-protobuf/
https://swift.org/getting-started
https://swift.org/getting-started/#using-the-package-manager

I remember reading recently that swift can be run in other platforms?
https://swift.org/about/#platform-support . That's cool!

Also, apparently we don't need XCode to do Swift development. But idk how
smooth it will be to do the development in a normal editor. XCode helps me
with so much errros - or may be it's the swift compiler's fetaures that XCode
uses. Idk. Gotta try some other editor for sure later

I got the `protoc-gen-swift` binary using homebrew

```
$ brew install swift-protobuf
```

I tried to import swift-protobuf package and for that I had to create a github token
and add it to MacOS accounts and then search the package in a UI? And it
wouldn't even show proper results and I finally added the swift-protobuf
package and to the target. Apparently there's a doc for it too
https://developer.apple.com/documentation/swift_packages/adding_package_dependencies_to_your_app
but I just managed it all by myself!

I also auto generated the swift file from proto using this

```
$ protoc --swift_out=. protos/MousePoint.proto
```

And before all this, I also created a directory called `protos` and that was
one hell of a ride :P I created something called a `group` and then later
moved that inside the main project directory as it was previously outside.
Anyways, finally, I'm able to create a value of struct of the message type `MousePoint`
that I created, that is, auto generated from the proto file ! :D

btw, I was able to get help info from `protoc-gen-swift` using this

```
$ protoc-gen-swift -h
```

and also check it's version!

```
$ protoc-gen-swift --version
protoc-gen-swift 1.8.0
```

---

Next I gotta check these links

https://github.com/grpc/grpc-swift
https://github.com/grpc/grpc-swift/blob/master/docs/quick-start.md

I got the grpc plugin for swift using this

```
$ brew install grpc-swift
```

but this installs `protoc-gen-swiftgrpc` and the repo says the name is
`protoc-gen-grpc-swift`. Might have to change the name if it doesn't work out
later!


---

All in all, some learnings:
1. I could really use some pre-installed binaries - and these exist in homebrew
but github repos are not mentioning them always
2. I could really try swift in VS Code or some other editor and do the building
and running and everything like package managing in the terminal. Not sure
how the experience would be - like in terms of - will it give me good errors
like something is not defined and how to automatically fix it with just a
button, and then also say "this has been replaced with this new thing" so that
I can use the new thing. Those are some good features I noticed in XCode, not
sure if it's XCode specific. Gotta see if other editors have plugins for
Swift and provide good UI/UX. Surely I don't want to be so stuck with XCode.
Damn I had to spend so much time to understand how to add a package
3. Of course I need to learn swift programming language. I am so so bad at it,
because I don't know a thing in it. I'm just making things work. Just making
things work. I haven't learn much at all!! 🙈 More like nothing. learned nothing!
4. Swift has REPL mode! Cool stuff!
5. Swift has some cool features like

```
$ swift run <swift-file>
```

Actually, the above is deprecated it seems. Instead we can use

```
$ swift <swift-file>
```

That's all for now I guess...


---

I checked the quick start in 

https://github.com/grpc/grpc-swift/blob/master/docs/quick-start.md

Still writing the code for it!

---

1. implement the server using the auto generated code
2. start the server
3. auto generate some swift client code or golang client code
4. call the server
5. call the server multiple times
6. see if you can change the input from single input to a stream input
7. how long can a service method be called? so that we can stream input
for a looooong time. check this. or else we will have to send mouse points
over multiple service method calls

---

So, I got this error about `CgRPC` module missing. It was weird and I checked
swift grpc and it had `CgRPC` in it's `Package.swift`. Later, I ran build and
then tons of errors compared to before. Now I see that the `CgRPC` module
has not been imported - due to multiple failures. It said something about

```
/Users/karuppiahn/Library/Developer/Xcode/DerivedData/controller-demo-bdfitjjlaospwpanjeouafyvtbhr/SourcePackages/checkouts/grpc-swift/Sources/CgRPC/include/src/core/tsi/ssl/session_cache/ssl_session.h:29:1: Import of C++ module 'BoringSSL' appears within extern "C" language linkage specification
```

And there were multiple such messages for multiple locations. Most of them had
the above as heading. I need to see how to fix it 🙈

So, I'm getting tons of errors and I'm also getting a warning about one library
`libnghttp2` and that it can be installed using `brew` with

```
$ brew install nghttp2
```

I just installed it. I think I need to update my `PATH` environment variable
too now

Actually, the errors didn't go away. I then updated `PATH` environment
variable 

```
echo 'export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> ~/.bash_profile
```

and removed the old statement I had for `openssl` and then I restarted XCode
and it worked!! :D 

I think it was something related to `openssl` and the `BoringSSL` module? Idk.
Anyways. Now. There are new errors! LOL 😆

Okay, so, I think I messed up something with respect to the accessor stuff.
Like private, public and all. So, initially I ran small `protoc` commands. Later
I updated it to include some more stuff, for example something about visibility
and made it public. But looks like I didn't make it public everywhere! Now,
I get this error

```
/Users/karuppiahn/oss/github.com/karuppiah7890/controller-demo/controller-demo/protos/Controller.grpc.swift:38:8: Method cannot be declared public because its parameter uses an internal type
```

And I get this error all over the place in my generated file - in 7 places,
where the code for the message type has been referred to. I think I need to
regenerate that code alone with public or do something else :P May be make
everything private or internal in this case :P I really need to learn swift!!!

Okay, I ran `protoc` commands to generate the code with public and everthing.
Now the old `BoringSSL` error has creeped back!! 🙈:/ Gotta check back later! 

---

Okay, so to ditch all the above issues, I think I'm going to use the latest
and greatest of the grpc-swift repo - 1.0.0 alpha release. I'm already doing
this and I noticed another issue. I forgot that I need to also use the same
version's binary and not an older version. Let me get the latest version
of the binary by building it from source

Did this -

```
$ # went into grpc-swift repo directory
$ gco '1.0.0-alpha.11'
$ make plugins
$ ./protoc-gen-swift --version
protoc-gen-swift 1.8.0
$ mv protoc-gen-grpc-swift /usr/local/bin/protoc-gen-grpc-swift
```

So, the `protoc-gen-swift` binary was good - I already had the latest, the
same as here, I just moved the `protoc-gen-grpc-swift` to overwrite the existing
binary. Let's get moving ;)

Okay. So, I regenerated the code using the new binary

```
$ protoc --grpc-swift_out=controller-demo/protos/ --grpc-swift_opt=Visibility=Public     --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
```

using the docs in my readme ;) and it all just worked - for a secondst the code
was not updated in XCode but later it got updated and then my build also ran
successfully ;) :D 

Okay. So, I copy pasted some code from these guides

https://github.com/grpc/grpc-swift/blob/master/docs/quick-start.md
https://github.com/grpc/grpc-swift/tree/master/Sources/Examples/RouteGuide
https://github.com/grpc/grpc-swift/blob/master/Sources/Examples/RouteGuide/Server/main.swift

Okay, so, now my server is runnnnning! :D :D It says

```
server started on port 61308
```

Now, I'm going to auto generate some golang code and see how to call this
server from the golang code! :)

So, I did this

```
$ protoc --go_out=controller-demo/protos/ \
    --proto_path=controller-demo/protos/ controller-demo/protos/MousePoint.proto

$ protoc --go_out=controller-demo/protos/ \
    --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
```

And that generated golang code in the repo. I started moving this to another
repo

I had to make some changes - for example rename the package in both the
generated files in the new project and also move them into a directory.

Looking at this now

https://github.com/grpc/grpc-go/tree/master/examples

And this file

https://github.com/grpc/grpc-go/blob/master/examples/helloworld/greeter_client/main.go

Okay, I think I should be using this module

https://pkg.go.dev/mod/google.golang.org/protobuf

and not

https://github.com/golang/protobuf

So, gonna do just that! including the code generation by my old protoc-gen-go
binary! 🙈

Using this to get the latest binary 

```
$ go get -u -v github.com/protocolbuffers/protobuf-go/cmd/protoc-gen-go
```

Okay, that failed with

```
../../../../go/src/github.com/protocolbuffers/protobuf-go/cmd/protoc-gen-go/main.go:21:2: use of internal package google.golang.org/protobuf/internal/version not allowed
```

So, I'm going to clone the code I think. Oh wait. They provide the binaries
in their releases! Yay! :)

https://github.com/protocolbuffers/protobuf-go/releases

https://github.com/protocolbuffers/protobuf-go/releases/tag/v1.21.0

https://github.com/protocolbuffers/protobuf-go/releases/download/v1.21.0/protoc-gen-go.v1.21.0.darwin.amd64.tar.gz

```
$ mv ~/Downloads/protoc-gen-go /usr/local/bin/
$ # as mac wouldn't allow the binary
$ sudo xattr -d com.apple.quarantine /usr/local/bin/protoc-gen-go
```

So, now I'm getting this error

```
$ protoc --go_out=controller-demo/protos/     --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
2020/04/30 21:37:17 WARNING: Missing 'go_package' option in "MousePoint.proto", please specify:
        option go_package = ".;MousePoint";
A future release of protoc-gen-go will require this be specified.
See https://developers.google.com/protocol-buffers/docs/reference/go-generated#package for more information.

2020/04/30 21:37:17 WARNING: Missing 'go_package' option in "Controller.proto", please specify:
        option go_package = ".;Controller";
A future release of protoc-gen-go will require this be specified.
See https://developers.google.com/protocol-buffers/docs/reference/go-generated#package for more information.

protoc-gen-go: Go package "." has inconsistent names MousePoint (MousePoint.proto) and Controller (Controller.proto)
--go_out: protoc-gen-go: Plugin failed with status code 1.
```

I'm gonna do what's mentioned here

https://developers.google.com/protocol-buffers/docs/reference/go-generated#package

which is mention an `option` like

```
option go_package = "example.com/foo/bar";
```

in my case

```
option go_package = "github.com/karuppiah7890/controller-demo-golang-client";
```

Now it says this

```
2020/04/30 21:43:00 WARNING: Malformed 'go_package' option in "MousePoint.proto", please specify:
        option go_package = "github.com/karuppiah7890/controller-demo-golang-client;controller_demo_golang_client";
A future release of protoc-gen-go will reject this.
See https://developers.google.com/protocol-buffers/docs/reference/go-generated#package for more information.
```

Oh. I see it. Package names cannot have hyphens. Oops. Let me change that. I
initially fixed it with it told me

```
option go_package = "github.com/karuppiah7890/controller-demo-golang-client;controller_demo_golang_client";
```

I changed it to this

```
option go_package = "github.com/karuppiah7890/controller-demo-golang-client/controller";
```

Now, it's all good. I think I'm even going to commit it to the repo. Just like that.

```
$ protoc --go_out=controller-demo/protos/     --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
$ protoc --go_out=controller-demo/protos/     --proto_path=controller-demo/protos/ controller-demo/protos/MousePoint.proto
```

I copied the code to the other repo. Trying to write the code now

Okay, after seeing the code, I just realized I made one mistake. I didn't
generate any grpc related code for rpc method. Only protobuf related code for
message type. Gotta fix that first!

Oh. So I tried this and it said to use something else

```
$ protoc --go_out=plugins=grpc:controller-demo/protos/     --proto_path=controller-dem
o/protos/ controller-demo/protos/Controller.proto
--go_out: protoc-gen-go: plugins are not supported; use 'protoc --go-grpc_out=...' to generate gRPC
```

Looks like the days are changing. Need to update my grpc demo here
https://github.com/karuppiah7890/grpc-demo/

Anyways. 

```
$ protoc --go-grpc_out=controller-demo/protos/     --proto_path=controller-demo/prot
os/ controller-demo/protos/Controller.proto
protoc-gen-go-grpc: program not found or is not executable
Please specify a program using absolute path or make sure the program is available in your PATH system variable
--go-grpc_out: protoc-gen-go-grpc: Plugin failed with status code 1.
```

Of course there's no `protoc-gen-go-grpc`. I need to see how this is done. From
what I remember, golang has only one plugin for protobuf stuff, unlike what I
saw for swift. Let me check what's going on

Checking this now

https://grpc.io/docs/quickstart/go/

Hmm. They say the same thing that I did before

https://grpc.io/docs/quickstart/go/#regenerate-grpc-code

Using the `--go_out=plugins=grpc:<abcd>`. That's weird

Okay. I did a cool move. Lol

```
$ cp /usr/local/bin/protoc-gen-go /usr/local/bin/protoc-gen-go-grpc
```

Or should I say cool copy? :P XD And it worked!

```
$ protoc --go-grpc_out=controller-demo/protos/     --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
```

Wait. But. No change in code. Okay. may be it didn't work. Gotta check why
later. Hmm. Damn. Didn't think my server would run and I would get stuck up
with auto generation of grpc client code for golang!!! Really, software
never ceases to surprise me!

Okay, quite some places are telling me to use a different `protoc-gen-go`
binary

https://grpc.io/docs/quickstart/go/#protocol-buffers

https://github.com/grpc/grpc-go/tree/master/examples#optional---rebuilding-the-generated-code

So, I'm doing this

```
$ rm -rfv /usr/local/bin/protoc-gen-go*
$ go get -u -v github.com/golang/protobuf/protoc-gen-go
```

WOWOOWOWOW! That just worked!!

```
$ protoc --go_out=plugins=grpc:controller-demo/protos/     --proto_path=controller-demo/protos/ controller-demo/protos/Controller.proto
```

And this time there was code change!!! :) :D

```
$ cp -r controller-demo/protos/github.com/karuppiah7890/controller-demo-golang-client/controller/ ../controller-demo-golang-client/controller/
```

And I wrote the code and ran the client with the server's port as input
and it all worked!! :D :D The mouse moved!! :D 

Demo : https://youtu.be/vH3cOqMJzo0
