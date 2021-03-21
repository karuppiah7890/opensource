# Recording Browser

I have been having a set of ideas related to collaboration tools for a long time

Most of these ideas are related to real time collaboration by two or maybe more
people. As the first steps to building these tools, I'm learning how to do some
basic things and some basic problems which I think are a bit part of the
bigger problem of collaboration tools

One of the problems that I keep thinking about is - how to record something?
Some action?

For example, how to record what I'm doing on a terminal? I can use a screen
recorder. It will create a video, in some video format like mp4. But that's
heavy weight. Asciinema tool can do it way better and light weight and the
resolution to play the recording is perfect unlike video resolutions - there's
also recording resolution which is what shows up in playing unless there was
editing done. At least that's what I know.

So, recording terminals, text editors, and any other tools is the idea that I
have for now.

As part of that, recording browser is the new idea. One can record using a
screen recording tool. And it will be perfect too.

But I want to record in a different and more light weight format. At least I
assume it's light weight. I don't know. I gotta check.

I have had similar ideas before but the repo that instilled more curiosity in
me was -

https://github.com/AditiTheCoder/Google-Search-Clone

This repo tells how we can check a .mov file to check the progress as a demo.

I was thinking how we can use a different kind of file to record web pages. But
yeah there can be disadvantages to recording a web page in the way I think. For
example, when recording a webpage by recording the HTML, CSS and Js in it, and
the changes in it, and maybe the mouse movements and clicks and what not, the
tricky part is, if you record in firefox and play it back on chrome, it might
look different as we would be rendering the web page using HTML, CSS and Js and
it may look different on different browsers. Unless it was taken care of as part
of the code. Also, another thing is - size. If we increase browser window size
or decrease it, the recording or the playing will get affected I think. Surely
the playing might be different. But that's not the case with videos. It's
always the same given the size of the player - small means smaller size, and
also if the resolution is same, it looks the same. So, yeah. Also, with
web page recording, only if done well maybe it can look the same in firefox I
think. Or else maybe even in firefox it might play bad even though it was
recorded on the same firefox (same version etc)

The only good thing about recording HTML, CSS, Js and stuff is, it will be light
weight. Or maybe it may not be light weight.

For example, if you want to record a web search engine image results web page,
and if the images have really high resolution, then your recording will store
all those images. It might get bigger than a video - maybe. Maybe. I just don't
know. Also, if you want, you can ignore storing images etc, and any and all
artifacts like Js, CSS. But the player may not work in some cases. Not sure.
The benefit of storing all the artifacts is that - you won't need Internet to
browse then! :) You just need the recording locally, offline. It will all work
fine. :) No need to have Internet. You can still play the recording. So, yeah.
It's an interesting problem I guess. Hmm

It will be a problem of thinking in terms of times and frames like movies. I'm
already solving a similar problem using web text editors

https://github.com/karuppiah7890/text-editor-recorder/

Let's see how that goes. I might work on this too! :) Some day! :)

---

Some notes from my notes app -

Should we really record the mouse? Yeah, to show mouse movement and clicks. Show a hovering mouse instead of using the real mouse. So, it's a complete web app

The tool will be built as an extension maybe

Do we have to store the Js? Hmm. If we store the Js, it will run in the user machine where playing happens and the JS can do anything then. For example security issues can arise due to this.

What are the advantages of having a Js stored as part of recording? Well, if we do clicks and if it does changes in the web page, we can see it dynamically. Some web pages only work with Js. However we will record the HTML - record every change in it as a delta and then apply it. If a Js is causing a change in HTML, we can see it with just HTML.

For example, some sites use cookies to store passwords, local storage to store information like if the website is in dark mode, if the email subscription popup has been shown etc. Now, apps use Js and do extra stuff based on this data. Also, this same data is also used to tell if a user is logged in or not.

Storing all this data (cookies, local storage, indexed db) is wrong. It can have sensitive information like personal info, secrets, credentials, tokens etc. So, if we don't store the data and if we store the Js, however the Js won't work. But, if we record HTML, even the popups will be recorded :) everything on the page is recorded. :) Every delta.

What about API calls made by JS? Well, JS won't be there. So, no API calls can happen! :) But, what about all the data that's obtained from API calls or all the data that is sent to servers via API calls? Well, sent data, we don't even need to know. We only need to record the browser, the UI of the app. If there was any data that was received from the servers via API calls, then based on that if any UI changed that would be recorded in the HTML recording. So, we are still good! :) Hmm. Also, if we did store JS, my idea was that we would use some worker or something and mock all and any API calls while playing the recording. Mock as in, just let it not go outside the browser and simply respond back or something. But I guess if JS doesn't receive right data, that is, same data, then it's problematic. Anyways, HTML recording for the win! :D

What about times when the user clicks a button? What about the effects of the button? If it's a soft mouse (web app mouse image etc) and not an actual mouse pointer, how to show the click? Maybe we can highlight the click with circles or actually click the button by capturing, recording and playing the clicks. One thing to note is, when buttons are clicked it's usually for some action. But, let's say if the button is to choose a file, like it's an input tag with type file. Then it's hard. Another window opens and things go wrong as our tool works only within that single window, single web app not outside of it in a file explorer to choose files. So that's something to understand. Maybe we can write javascript code to have a click listener for all elements and prevent the click event from happening. Let's see. Or we can simply leave such cases for fixing latee :) If we don't handle it now, the playing continues but the file explorer is open till user closes it - this is when we simulate user's click actions on the web page. Actual click or simulation click can help visualize some things ! :) Like button click feel - graying out or dark color and then change in color etc

What about CSS? Record CSS too. But I think Js cannot change CSS file. But it can add some css differently I think. Idk. Like, adding in HTML. Then HTML recording is enough.

Sometimes apps have many CSS files compiled into one CSS file or something. So, just store all of them. Only then the site will look nice!! Browser will take care of rendering the HTML with CSS! :)

How to record HTML in a site? Hmm. Use some shadow Dom or virtual Dom or some concept and capture all changes in dom and store it as diff similar to how react changes HTML only ij diffs efficiently. We can do something similar! :)

Record mouse movements too by putting a listener on html or body tag maybe

Open source tool for trust

Completely offline tool. Doesn't steal passwords etc. Records and plays offline too.

The user has to understand that they are recording and should not store or have any sensitive information in the web page.

How to record user input? We spoke about clicks. What about typing? Hmm. Focusing on elements with mouse or keyboard with tab key or something? Hover action capture? Hmm
