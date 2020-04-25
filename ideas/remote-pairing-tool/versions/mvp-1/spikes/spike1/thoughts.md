Spike 1: How does one capture the actions of a mouse and details of a mouse?
What's possible and what's not possible? Does one need a blank window to
capture a mouse? Can it be done with no windows? That is, no GUI, at all.
What are the limits to capturing the mouse's actions? When can we do it and
when can't we? As usual explore a lot to checkout the unknown unknowns.

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
