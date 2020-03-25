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
