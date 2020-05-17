# Real time collaboration. Real time communication. Real time stuff

Peer to Peer (P2P) vs Central servers?

Tech? WebRTC, IPFS (orbitdb etc), GunDB?
Bit torrent? Raft? Dat project?
Websockets?

Paid - Firebase

Environments to run in? Constraints? Requirements?

Some thoughts on Requirements:
1. Chat app. Some questions around that:
    - With ability to see history completely vs not completely? especially after disconnect.
    - Should history be maintained forever even after all users disconnect? or 0 history?
    - Is it like slack? Meaning full history and everything maintained. Chat rooms, etc.
    Slack alternative might be a bad idea. There's already mattermost and many others.
    Simple chat for quick simple text messages is enough I think. But yes, we need to
    define the boundaries so that we don't build slack. 🤣
    - Or is it like temporary chat? Which goes away after everyone logs off?
    - Ability to delete sent chat messages? Ability to edit sent chat messages?
2. Support atleast 2 users. Can think about more users later
3. Voice or Audio chat?
4. Video chat?

Does the whole session depend on any single user?
In case of pair programming, if the host (main user) itself is out, then?
It does not make sense to let someone remote control the host's machine even if
it's possible until the host is active. Ideally, host is active means they are
online and their computer can be remote controlled and their computer's files
will be used for the code pairing session. So, it depends on the use case.
For example in google docs, there's no dependency, since the doc is stored in
the cloud.

For remote pairing, do we want to let the other users have the whole of the
repository in their machine? Or at least the docs which are open in all the
tabs. That way, if host's machine crashes for some reason, may be the other
user can help? Gotta see if central servers should help or not. Technically they
can, but it's a question of privacy too. Hmm. Probably we can give an option for
that and they can enabled or disable it may be? Hmm.

---

Some more databases and stuff I noticed when checking about CRDT and more


Conflict-Free Replicated Data Types (CRDTs) - https://www.youtube.com/watch?v=ZLjl_55um4I

https://www.youtube.com/channel/UC8LJKi0UlvZygUMC8wsKFEQ
https://medium.com/offline-camp

https://www.youtube.com/watch?v=B5NULPSiOGw

https://couchdb.apache.org/
https://blog.couchdb.org/
https://docs.couchdb.org/en/stable/

https://riak.com/

---

RGA ? What's that? Find out? Something related to text editing
https://duckduckgo.com/?q=RGA+CRDT+algorithm&t=ffab&ia=web

Verifying strong eventual consistency in distributed systems
https://dl.acm.org/doi/10.1145/3133933
https://dl.acm.org/doi/pdf/10.1145/3133933

A Conflict-Free Replicated JSON Datatype research paper
https://arxiv.org/abs/1608.03960
https://arxiv.org/pdf/1608.03960


---

Full Ecosystem:
https://github.com/automerge

Data layer based on CRDT concepts:
https://github.com/automerge/automerge
https://github.com/automerge/automerge-rs

Network layer:
https://github.com/automerge/hypermerge (Based on hypercore/Dat)
https://github.com/automerge/mpl (Based on webrtc)
Other possible network layers: Websockets

Apps:
https://github.com/automerge/pixelpusher
https://github.com/automerge/trellis

Slack: https://automerge.slack.com

---

Real time collaboration for jupyter

https://github.com/jupyterlab/rtc

---

Conflict-Free Replicated Data Types (CRDT) for Distributed JavaScript Apps.
https://www.youtube.com/watch?v=M8-WFTjZoA0

---

https://pouchdb.com/

---

So, I'm thinking of creating a basic to do app may be? To start with?
To play with different solutions. But yeah, it won't be close to what I need
to do for text collaboration. I think I need to work on that too. Yeah.
Hmm. A peer to peer, to do app sounds fun, yes. Especially with offline support!
:) Anyways, I think I'll try the text collaboration thing first I think :)
May be show a list of versions and all for every change and stuff.
Use different kinds of networks like - dat, ipfs, webrtc, websockets, to see
how it all goes? To start with, may be dat and webrtc I guess. Let's see.

One thing to note is - I don't know if I need all the changes of the document -
if all the peers have the same document at some point? But, well, that's not
for sure. People could keep changing the document. So, I guess we just have to
keep it up. But, what if we can compress the very very old changes? That both
the peers have? That way, we have lesser stuff in the history - history size
is less - actually, more like, aggregate all the changes of the past, and make
it as one change - I don't know. It sounds good, but idk how it would be done.
I just gotta see what downsides the history will have - because there's a lot
of history for the changes, so yeah. Especially for text, it looks like the
changes are at character level - more like a character that you can see. Hmm.
Anyways, I'm sure I'm going to figure it out! :) 

In this video - https://www.youtube.com/watch?v=M8-WFTjZoA0 , they talk about
how some old data (tombstones) take up a lot of memory, and how we can get rid
of it - but that's possible only if all the peers are online and the process
has to happen at the same time - since we are getting rid of it, as we don't
need it - it's like garbage, so, he calls it garbage collection, the usual
programming term. So, some garbage collection protocol, and if all peers are
online, which is not easy to ensure if you don't know who are the peers and what
is the total number of peers or if there is even any concept of total peers,
especially in a completely peer to peer system. Anyways, even if we can say
that all necessary peers are online, to perform garbage collection, while the
peers are editing too - as you cannot stop the peer and say program wants to
do some clean up - so while they are still editing, I "guess" all peers could
agree upon the same set of old data, that they want to get rid of, and then
get rid of it at once? That seems like a very basic idea. I might look it up
later after understanding more about the premise, because I didn't hear about
the word "tombstone" in CRDT premises/context. Anyways, I still want to get
rid of very very old changes somehow, as mentioned above. 

Okay, looks like "tombstones" concept is part of Operational Transformations (OTs).

---

https://libp2p.io/
https://github.com/libp2p/libp2p

---

https://github.com/search?utf8=%E2%9C%93&q=hypercore
https://github.com/hyperswarm
https://github.com/datrs
https://github.com/mafintosh/hypercore
https://dat.foundation/explore/projects/
https://github.com/datproject/dat

https://github.com/cabal-club

---
https://ace.c9.io/
https://codemirror.net/

---

https://arxiv.org/search/?query=crdt&searchtype=all&source=header
https://arxiv.org/search/?searchtype=author&query=Kleppmann%2C+M
