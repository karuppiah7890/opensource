# thoughts

Some random thoughts on what to implement or what should be part of the tool.

* In one remote pairing session, only one computer, let's say computer A, is
being controlled, but by many people from multiple computers, and also by the
person using computer A. For the first version of the app, we can assume that
there are only two users totally controlling computer A, one user owns
computer A, other user is remotely accessing computer A.

* What kind of controls are we looking at? The two basic inputs that I know are
mouse and keyboard. There are other inputs like [light pen](https://en.wikipedia.org/wiki/Light_pen)
and probably more that I don't know about. And I don't even know which ones are
still relevant and being used in the industry. But for simplicity's sake, I'm
going to start with just focusing on mouse and keyboard. Probably if I get
requests from users for other kinds of inputs, I can think about them at that
time.

    Even with mouse - I would like to stick to just left click and right click.
    I'll see if I can bring in the middle button click too. I primarily use a
    laptop and am not sure how the middle button click even works here and have
    never used it. May be I can get my handy mouse that I haven't used for a
    long time to may be help with the middle button feature. But for MVP, only
    left click and right click will be taken into consideration.

    For keyboard, I need to see how to handle simple keys like alphabets and
    numbers and then some special keys like escape, space and what not. And
    also check how to handle single key press and then multiple key press -
    especially in programming, there's usually a lot of multiple key press.
    Also, make sure that the key presses on the remote user's computer are
    captured and only triggered in computer A, and not in the remote user's
    computer. In Zoom I have noticed that my remote control is toggled on and
    off based on an event - I need to click on the zoom window which shows the
    other user's screen, and only after that I can control their computer, and
    I think if I click out of that window anywhere, I lose control and I can
    continue controlling my own computer. These are some things to note

    For the first version, based on complexity, we can have two mouse pointers
    for two people - or just one mouse pointer being controlled by two people,
    one person at a time, or else it will be havoc :P I'll do my research on
    this and decide

    For screen sharing, I think we need to provide a window to the remote user
    to be able to see computer A's screen, and then control it. It's more like
    screen recording / video recording the computer A's screen and then
    streaming it to the remote user. I can't think of a better analogy.
    Apparently there are already some tools and protocols that help with this.
    I would like to research about them

* To be able to work smartly and effectively, I think more research is better.
I also read today about how it's better to check the history and do some
past research before doing some work over here -
https://jlongster.com/How-I-Became-Better-Programmer . It tells about how you
can get the help of the past research. Another thing that I usually read is -
stand on top of big shoulders - libraries, protocols, frameworks and what not,
that have been developed for years based on experiences, which is a lot of
effort, which I don't have to do or reinvent the wheel in those areas, unless
I want to experiment or think I can do better or just like that. So, I guess
I'll checkout some papers, libraries and protocols and also try my own ideas
and thoughts

* About audio of user, video of user, chat feature - all that is secondary for
now and are a big problem by themselves. Let's see how we get there! :)

* If only terminal has to be shared, checkout solutions like https://tmate.io ,
and others, which are based on tmux

* Check about Virtual Network Computing (VNC) server to see screen

* Check about the tools I have put up in the [tools list](../remote-pairing-tool.md)

Action items
1. Read existing research papers on screen sharing
2. Check existing tools, libraries and frameworks that help with screen
recording, and more. A list -
    * [OBS](https://obsproject.com/) - helps with recording screen, streaming to
YouTube. Source code - https://github.com/obsproject/obs-studio

    * [Kap](https://getkap.co/) - helps with recording screen. I have noticed
    that it records at a really high resolution and can also provide lots of
    frames per second (fps). I still need to learn more about these terms,
    but yeah, those are some of it's features. Source code links -
    https://github.com/wulkano/kap - Kap source code. Behind the scenes, they
    use https://github.com/wulkano/Aperture - to record the screen on macos.

    * [webrtc](https://webrtc.org/) - Long ago I remember using webrtc to create
    a peer to peer video chat in the browser -
    https://github.com/karuppiah7890/p2p-videochat .
    Firefox and Chrome support WebRTC and it includes - Audio, Video and Screen
    Sharing as part of it's Real Time Communication (RTC). Some more links -
    https://en.wikipedia.org/wiki/WebRTC
    https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API
    https://webrtc.github.io/webrtc-org/
    https://www.html5rocks.com/en/tutorials/webrtc/basics/
    https://www.npmjs.com/package/simple-peer

    * In case I start thinking about multiple people controlling someone's
    screen - some more things to look on are peer to peer data sharing, where
    data denotes - any data - computer A's screen's video, mouse movement
    data, and more like audio, video, if that's there too. If it's peer to peer,
    there are some benefits to it. I think it might have cons too, just that I
    don't know much and can't think of much. Some things on peer to peer data
    sharing - webtorrent, torrent, bittorrent protocol, dat project etc . Links
    - https://github.com/anacrolix/torrent ,
    https://github.com/webtorrent/webtorrent , https://github.com/webtorrent ,
    https://dat.foundation/ , https://github.com/datproject/dat ,
    https://github.com/datproject , https://blog.datproject.org/ ,
    https://beakerbrowser.com , https://github.com/beakerbrowser/beaker .
    Check these good links to understand if peer to peer (p2p) protocols,
    techniques and technologies can help ! :)


---

Discussion with a colleague while trying out things

VS Code Live Share

connects to a server. microsoft servers

---

OBS - show my screen to someone else

separate app - remote mouse and keyboard
control

zoom: transmit it as an image. 

vs code : just update the diff in each file.
it doesn't render.

difference between full screen share, versus
in-app data and render it with client
intelligence

in case of vs code it's a lot better.

zoom - your keystrokes to the other
person's machine. remote keyboard control.

keystrokes - cumbersome. lot of the
keyboard shortcuts could be system shortcuts

around - a tool. startup. focussed work.
not very intrusive. 

end users - developers?

extend to creators?

native support - possible?

platform / app should support plugins

or else piggyback with tools like zoom,
which works on full system - less secure.

---

The broad set of features we are looking at might be -
1. Be able to view another person's screen in my computer
2. Be able to talk to the other person - this might be key as in,
I can't simply be seeing their computer. To communicate, I need
something. Or else the other person has to use text - write text
on their computer in some text editor may be to communicate with me
and even then, I can't talk to them unless I have remote control or
something. So, audio call is key
3. Be able to control the mouse and keyboard of the other person -
some things to note are - when I have a shortcut XYZ in my machine
which does RST in my machine, and the other person also has XYZ
shortcut in their machine, and that does MNO in their machine,
what should happen? And what if XYZ is a shortcut for the remote
pairing tool? Such keyboard shortcut clashes need to be taken
care of. When which shortcut kicks off needs to be decided or
give option to user since we cannot detect such stuff I think.
Most probably we need some way to say, when the focus is on
remote pairing, that is, when I'm having my mouse/keyboard
focus in their computer and type XYZ shortcut, it should 
effectively be something happening in their computer,
and may be the remote pairing tool can think about how to
provide shortcuts in such a way that there are no clashes,
or may be just not provide any shortcuts. 
4. Be able to video chat with the person - this is not very
key. It's a good to have though
5. Be able to text chat with the person. This is cool as in,
this way, you can send some text or links to the other person
while pairing
6. Be able to do stuff with multiple cursors like google docs.
I think this is awesome. Multiple cursors and all. Not sure
how much of it is possible. But it's awesome as, it makes
sure you don't have any problems moving around your mouse,
while the other person is also moving it around. And also,
no issues with both of you typing. You can both simultaneously
type
7. Be able to run the tool in any platform. Any is too broad,
so, majorly - MacOS, Linux and Windows. Not sure if we can
easily support mobile devices and tablets, and how the UI/UX will be.
But yeah, that's a possibility too
8. Be able to control the other person's computer very
smoothly. This is key, as no one wants lag
9. Be able to clearly hear the other person with no noise
10. Be able to tell if there are any network issues causing
disruption to the communication and collaboration
11. Be able to see the video of the other person quite
clearly
12. Be able to securely do everything, with no fear that
someone could tap into our communication or hack our computers
and do remote control and remote code execution. Security
must be tight to NOT allow intruders. And all communications
must be encrypted end to end, so that no one can tap it in
between. Even the servers helping me to communicate should NOT
know what I'm communicating and also, it should NOT know
who I'm communicating with. Ideally it should NOT know
anything and just help to communicate with the other person.
This way, if someone hacks the server, they cannot know who
I communicated with and collaborated with and so on. The idea
is to keep the server as dumb as possible - without too much
data, but just enough to help serve the users.
13. Be able to host the servers myself given a documentation.
Be able to host it very well and maintain it too, very
easily.
14. Be able to upgrade all the softwares - client and servers,
very easily with no downtime.
15. Be able to tell metrics regarding my communication with
the other person - like the lag details, Internet bandwidth
being used. Any metrics that the user can see to understand
problems in any case any occurs or to just know some speed
information.

---

Be able to view another person's screen in my computer:

* The most basic solution I can think of for this feature alone is
OBS - https://obsproject.com/ , https://github.com/obsproject/obs-studio .
It can capture your screen, and stream it to streaming services like
YouTube, Twitch and more! It can also capture your audio, video too!
It's like the perfect thing for webinars / virtual meetups. You can
also do some processing for your video - add banners and all, and do
things like noise cancellation for your audio. Those are the features
that it has


* Another way to share your screen, and also do audio/video calls is
using WebRTC - https://webrtc.org/ . With WebRTC, you can also share
random data with the other person - like chat or anything! With WebRTC,
you can do screen share with multiple people, and also do audio and
video calls with multiple people. Examples - appear.in , google meet.
Also, in screen share, you can share your whole screen or just a
particular window :)

https://en.wikipedia.org/wiki/WebRTC
https://webrtc.github.io/webrtc-org/
https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API
https://www.html5rocks.com/en/tutorials/webrtc/basics/
https://www.youtube.com/watch?v=BVBXkzVjvPc
https://www.npmjs.com/package/simple-peer
https://www.youtube.com/watch?v=aVgH-mVdS6s
https://www.youtube.com/watch?v=PT8s_IVWDgw
https://www.youtube.com/watch?v=g1GG7kT46l4
Names: "Feross Aboukhadijeh"
https://www.youtube.com/watch?v=2qrUx-C5Np4
https://www.youtube.com/watch?v=kxHRATfvnlw
https://www.youtube.com/user/FreeTheFeross
https://www.youtube.com/watch?v=aqnvKP1DYRI

extension sample - https://chrome.google.com/webstore/detail/webrtc-control/fjkmabmdepjfammlpliljpnbhleegehm

video chat sample - https://github.com/karuppiah7890/p2p-videochat .
Not sure if it still works. 


With WebRTC - things are lightweight is my guess. And it makes use of
the well known platform - the browser. The browser runs on SO many
devices. You just don't have to worry about cross platform!

---

Be able to control the mouse and keyboard of the other person -

Currently, for this, I have only tried Zoom. There are so many
other tools that can help with this. I tried VS Code Live Share
too recently actually. The experience was good. I mean, I was
able to work with my friend well within the VS Code Editor - more like
a sandboxed environment than be able to have access to the
whole computer. My friend was able to edit a file with me.
She was able to independently edit the document with her
own cursor and I was also independently able to edit
the document. So, multiple cursor support was cool, and
yes, the keyboard support too. And my friend was also
able to get access to the bash terminal and type into
that too! It was cool :)

There are other tool too! Like tuple.app

---

Be able to video chat with the person

WebRTC, Zoom, Google Meet, appear.in, Google Duo and so many more

---

Be able to text chat with the person

Slack, Google Chat, WhatsApp, FB messenger, Signal App, and so many more

---

Terminal Sharing based on tmux - https://tmate.io

---

MacOS `Screen Sharing` app for sharing 
screen. Native App. It also has support
for remote mouse control and keyboard
control I believe.

---

Technologies - Virtual Network Computing
(VNC); Remote Framebuffer (RFB) protocol;

https://github.com/karuppiah7890/rfb-protocol

---
