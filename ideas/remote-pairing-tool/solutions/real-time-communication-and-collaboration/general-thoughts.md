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
