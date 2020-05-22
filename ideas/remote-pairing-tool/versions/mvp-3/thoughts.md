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


