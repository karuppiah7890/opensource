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

There's a section called `Controlling the Mouse Cursor` here! And there's this
thing called `CGGetLastMouseDelta()`

https://developer.apple.com/documentation/coregraphics/2437197-cggetlastmousedelta

Gotta check how that helps. Also, in this page, they recommend checking `NSEvent`
class for tracking mouse

https://developer.apple.com/documentation/appkit/nsevent 

I think I'll be checking this out

https://developer.apple.com/documentation/appkit/nsevent/1532495-mouseevent

Let's see how that goes!

