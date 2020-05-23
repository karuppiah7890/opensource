Going to work on the code over here 

https://github.com/karuppiah7890/vs-code-pair-with-me

I'm first going to incorporate and use these

https://github.com/atom/teletype-crdt
https://github.com/atom/teletype-client
https://github.com/atom/teletype-server

I'm not going to worry about - if it's fast or slow or whatever. Just trying to
get something to work to get an idea about what's going on and what to expect :)
and also understand how to integrate with the VS Code editor - the edting, the
multi cursor and so on

---

First thing to do is - check how teletype works! The libraries, client and
server.

Okay, first things first. Teletype is actually a separate package. There's not
really much code referring to the word `teletype` in the `atom` codebase, and
that's when I realized I installed it as a separate package and that it wasn't
built in. It's a cool thing you know? I love Atom I think ;) I can see a lot
of it's core features in the packages under this section called `Core Packages`.
Shows how modular their features are and that people can toggle off even the
core features if they want to! :) At first I had a different opinion, but in
terms of code and modularity and may be even simplicity, I think this is cool!
Separate independent modules!

I also found out the codebase for the teletype atom package

https://github.com/atom/teletype

And in [`teletype-client`](https://github.com/atom/teletype), they describe it as

```
Editor-agnostic library managing client interaction for peer-to-peer collaborative editing in Teletype for Atom 
```

It's cool that it's editor agnostic. I gotta see how. Hopefully I can easily
plug and play this with VS Code. Let's see! :)

Unfortunately, in all repos, I see that the documentation is missing for the
APIs and is under the TODO. So, I gotta read all the code now 😅So, gonna do
that! Gotta dig into the code! :)

I noticed a `doc` directory. They have some RFCs (Request For Comments). I'm
reading those now, to understand stuff :) This is nice!

The RFCs are really really good. I had some thoughts on some overview of these.
I can see some elaborate thoughs and features that have been implemented. It's
nice to see something like this :D :D

I was reading some more of the RFCs. In between I started browsing just like that
and noticed some more open source extensions for brackets, sublime and one WIP
one for vscode too. I tried the web version of brackets extension - frankly, it
had some issues. That was unfortunate. Anyways, I noted down the list of tools
[here](../../existing-tools.md)

Reading the RFCs, I'm having some thoughts, ideas and realizations. For example:
1. The number of steps needed to start collaborating - it's better if it's
as little as possible
2. What if the other person doesn't have the extension installed? Are they
prompted to install? How?
3. What if the extension versions of both the users are different? As a
developer, we need to think about compatibility between versions and see how to
force upgrade if we have a need to, or support older versions without much
issues. But of course, older versions will not get new features. And for bug
fixes, especially security bug fixes, we might have to try to force upgrade!

Now, I'm checking the source code. I thought I could start reading from the
first release of the source code and see what features they built a bit, and
then see the master branch source code

Okay. The code is a bit readable, but since I don't know the way atom packages
work, I'm still trying to understand what's going on. I can see an `activate()`
function which is having some functions that are getting registered to the
atom commands in the command paletter I think - "Share portal", "Join portal",
"Close portal".

I can see quite some code from `teletype-client` being used. I guess I'm going
to already start seeing what the latest code looks like and then try to
understand how it works with Atom by understanding a bit of Atom packages.

Now I'm checking the latest code. It's a lot of code. I was checking how the
authentication happens with GitHub. I actually now forgot how I did it. I might
have to uninstall teletype and reinstall to find out how I did it. I think I
used personal access token, but I'm not sure, and looking at the list of my
personal access tokens, I think I'm reusing the same token in many places? Or
named them badly

https://github.com/settings/tokens

I can see `keytar` being used for storing credentials

https://www.npmjs.com/package/keytar

It's one of the strategies to store credentials. And `keytar` actually is used
to manage the system keychain and it supports the three major operating systems
which is MacOS, Linux and Windows. In MacOS I can see the oauth token being
stored in the `Keychain Access` software under the name `atom-teletype` and of
kind `application password`. 

And like I said, it's only one of the strategies. The other strategies are
`Security Binary Strategy` and `In Memory Strategy` to store credentials in the
credentials cache. As the name suggests, for `In Memory`, it stays only during
the lifetime of the current window, that is, when it's in the memory / RAM and
then it's gone. The `Map` data structure is used here, so I think it's alive
only till the program is alive and available within it's scope, and then it's
gone I guess.

The `Security Binary Strategy` seems to be valid only for `darwin`, that is,
MacOS. I guess it makes sense and is possible in MacOS. I'm checking why. Okay,
as the name suggests, it's about the binary in MacOS called `security`. They
execute some commands and use it. I think it's like some command line API to
the keychain in MacOS? Not entirely sure. But yeah, it's one way to store
credentials, an extra way for MacOS alone.

And all of it looks more like a key value store. You give a key, and then
a secret value. And all of the above strategies work that way or have a
provision to work that way I guess.

For `security` binary, the commands used are

```bash
# for setting / adding a key and it's value
$ security add-generic-password -s dummy-service-name -a dummy-key-name -w dummy-value -U
# for getting a key's value
$ security find-generic-password -s dummy-service-name -a dummy-key-name -w
dummy-value
# for deleting a key and it's value
$ security delete-generic-password -s dummy-service-name -a dummy-key-name
keychain: "/Users/karuppiahn/Library/Keychains/login.keychain-db"
version: 512
class: "genp"
attributes:
    0x00000007 <blob>="dummy-service-name"
    0x00000008 <blob>=<NULL>
    "acct"<blob>="dummy-key-name"
    "cdat"<timedate>=0x32303230303532333038303733325A00  "20200523080732Z\000"
    "crtr"<uint32>=<NULL>
    "cusi"<sint32>=<NULL>
    "desc"<blob>=<NULL>
    "gena"<blob>=<NULL>
    "icmt"<blob>=<NULL>
    "invi"<sint32>=<NULL>
    "mdat"<timedate>=0x32303230303532333038303830375A00  "20200523080807Z\000"
    "nega"<sint32>=<NULL>
    "prot"<blob>=<NULL>
    "scrp"<sint32>=<NULL>
    "svce"<blob>="dummy-service-name"
    "type"<uint32>=<NULL>
password has been deleted.
```

Also, I also checked the `Keychain Access` program after adding it, modifying it
and after deleting it too. It was there, and then it got modified and it got
deleted too later. So, like I thought, more like a command line interface to
the system's keychain and `Keychain Access` is the GUI access. I can also
see where the keychain is present while deleting it. I also saw this

```bash
$ security list-keychains
    "/Users/karuppiahn/Library/Keychains/login.keychain-db"
    "/Library/Keychains/System.keychain"
```

I guess it's pretty cool. `security` seems to have quite some features. For
now I'm not gonna dig into it I guess.

I'll just keep it in mind that we are going to use the OS keychain to store the
oauth token of GitHub and that's it :)

Actually, the name of the secret is being called `oauth-token`. Hmm. My bad, I
guess it's different from a personal access token. Weirdly I don't see the
GitHub App in my GitHub Apps list. Let me go check that first

Oh. I was looking at the wrong place. Of course I didn't have just one
authorized app in my list which I was seeing. Found it here

https://github.com/settings/applications

It was called Teletype for Atom. Yup. It was through OAuth and not a personal
access token.

Okay, I'll check how the authentication is happening now. And how those cute
avatars come ;)

Btw, with respect to `keytar`, I don't find `keytar` in the `package.json`. I
think Atom has it built in, in it's source code, in it's `package.json`? Yeah,
I see it `https://github.com/atom/atom` codebase in the `package-lock.json`
under `github` package which is actually this package over here -
https://github.com/atom/github . It's the Git and GitHub integration package
for Atom.

Looks like the `teletype-client` is used for the signin process, by giving
in the `token`. 

Okay, just now I tried out the login mechanism in Atom, by revoking OAuth
access for `Teletype for Atom` application. It asked me to login this time,
at `teletype.atom.io/login` and the usual OAuth mechanism happened. I got
redirected to the github oauth page, where it got read access to my data to
identify me. And then it showed me a token, which it asked me to copy and
paste in Atom. And I did it and it worked.

I can't remember how I did it in VS Code. I guess I need to start analysing the
tools and note down their UX, behavior and all and learn from them and note
down everything! :) Hmm. I did understand some stuff in each tool, but I think
these tools have a looot in them! :)

Okay, back to how the authentication happens - I found it out. So, of course
things don't happen the way I imagined, because for that token would be needed,
and no place token was set in the code I walked through except one place, but
I had no idea who was passing in the token. Later I realized in terms of the UI,
it was me who was giving the token as input, so I used the UI placeholder and
other text to find the UI component and found out that it calls the signin
method in the authentication provider using the token, and the signin method
does stuff like signing in with the token and then setting the credentials cache
to store the token.

I guess the first thing to do over here is, create a UI for the same in VS
Code. Hmm. Also, may be check how VS Code Live Share has it's UI and user
experience. May be we can keep it simpler? Idk.

VS Code Live Share does not ask it's users to do a copy paste of the token,
but there's a facility to do so, if the automatic thing doesn't work. I need
to see how to detect the code automatically. Hmm.

Also, in VS Code, once the tokens are used, they become invalid - expired.
Unlike in Atom, where I was able to use the token again and again. Hmm.
Not so good actually 😅Like, just in case someone sees my token. Hmm.
And I was recording a video to see the experience. So, I had to actually remove
the OAuth app - that is, revoke access and then allow access again, and then
only the old tokens became invalid and only the new tokens worked :)

Okay, so I tried the VS Code Live Share extension some more now. I noticed that
when the extension is enabled in one session and you go and invite another
person - if their extension is not enabled, nothing shows up. You can just see
an exclamation sign near the root directory name / project name, I don't know
how that alone got leaked, not sure, but other than that, I could not see files,
directories, or things like Live Chat and all. Later, I enabled it and then saw
it all reload and come up at once.

It had features like kicking out participants, or things like participants
leaving the collaboration session. And anyone can focus everyone on a single
file using `Focus Participants` feature. It was actually pretty cool. And for
multi cursor, only when you get into a new file tab, it would show the cursor
and the name of the other person, and the cursor will be colored. And after that
I tried hard to hover over the cursor and see names, but couldn't. It actually
showed initially, but never later. It showed later only when the tab was closed
and opened, and it was shown the first time alone.

Apparently VS Code also has some cap on the number of people who can collaborate.
It's a big number only though - 30. Pretty useful for pair programming, but
if you have some coding class or tutorial class and have too many read-only
sessions, you might need more than 30. Not sure though. Hmm. CodePen has this
pro feature for collab mode, which is short for collaboration mode.

One weird thing I noticed is, in the VS Code Live Share Chat, I was able to
see different avatar in one workspace and totally different one in another.
I think one of them is based on my microsoft account and the other is based on
my GitHub. Just a guess, as I can't remember which account I initially linked
it with.

For UI, Live Share uses the bottom status bar, to show the identity of the
user and uses the notifications to show non-finite progress - it just keeps
moving around to show that something's going on.

It also uses an extra view on the explorer to show some things regarding the
Live Share. And there's a separate section for it on the left which also has
almost the same details and it's called Session details. And there's some extra
stuff here - Recent Contacts, Suggested Contacts, Reporting bugs, Configuring
Settings, Giving Feedback. 

Configuring Settings - I can see quite some settings! For example - showing
Live Share status in the status bar - always, never or only while collaborating.
And some more stuff

I gotta see what I wanna do now. Hmm. 

I think I'll read some more code to see how the authentication happens and
what happens next - like sharing code / workspace, joining portal. And may be
start thinking of a minimalistic UI for a start for those things, including
login!

Phew! Lots of code. Overwhelms me. One thing is for sure - I have to understand
and write lots of code for even the view part and stuff and integrate it with
`teletype-client`, at least that's the current idea. I'm still trying to
understand their terminologies and working. I also gotta see if I can implement
the same in VS Code. Hmm. Let's see. 

By the way, for the avatar, that is, my DP - display picture, I just need to
use this URL - `https://avatars.githubusercontent.com/${login}` and that's it!

For example - https://avatars.githubusercontent.com/karuppiah7890 is my avatar
for my `karuppiah7890` github account. This is nice! :) Hmm. And anyone can see
it I guess, like, request for it, given login username. Anyways, I don't think
I'm going to show avatar anywhere, or any fancy UI. Most probably it's all going
to be very very basic UI to start with. And fancy stuff, I'll check later! :)

I think I need to understand the features that `teletype-client` is providing
and then yeah, of course come back and see how `teletype` uses this and I
gotta understand how `teletype-server` and `teletype-crdt` play a role in this
whole thing. In short, I want to understand how the whole stack works, to be
able to understand the architecture and working and may be replicate it, or
else, write some stuff of my own if nothign suits me. But I think I should start
with this code, no matter what, and write as little code as possible! :)

