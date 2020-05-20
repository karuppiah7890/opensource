For real time collaboration on docs, I started digging into things

https://github.com/stas-sl/realtime-collaboration-resources

"Spacetime Characterization of Real-Time Collaborative Editing" -
https://upsilon.cc/~zack/research/publications/cscw-2018-rtce.pdf

https://www.smartsheet.com/document-collaboration

open source solutions:
1.  https://etherpad.org/

---
Found another tool in market Code Together -
https://marketplace.visualstudio.com/items?itemName=genuitecllc.codetogether
https://github.com/Genuitec/CodeTogether - issues alone
https://www.codetogether.com
https://www.codetogether.com/download/
https://www.codetogether.com/pricing/

It has support for IntelliJ, VS Code and Eclipse. Nice

They have a free plan!! :D 

---

Firepad - based on Firebase. Open Source

https://firepad.io/
https://github.com/FirebaseExtended/firepad

What I could check is - how does it work? Apparently it uses some code editor
softwares like CodeMirror and Ace.  https://codemirror.net/ https://ace.c9.io/
But that will come by default for visual
studio code and other editors if I'm building it as a plugin to an editor. 
And I gotta see how it works along with Firebase. May be I could plugin
something else instead of Firebase, something for which I don't have to pay too
much. Let's see. Of course it comes at maintenance cost. Hmm.

The demo works quite well.

---

Demo didn't work out well for me. https://blindpad.github.io/

https://github.com/blindpad/blindpad

---

http://www.laktek.com/2010/05/25/real-time-collaborative-editing-with-websockets-node-js-redis/
https://github.com/laktek/realie

More:

https://github.com/search?l=JavaScript&q=collaborative+editor&type=Repositories
https://github.com/search?l=TypeScript&q=collaborative+editor&type=Repositories

https://github.com/ritzyed/ritzy
https://github.com/gobby/gobby
https://github.com/ckeditor/ckeditor5 , https://ckeditor.com/ckeditor-5
https://github.com/mattkrick/rich
https://github.com/ekuiter/variED , http://varied.herokuapp.com/#/
https://github.com/Maplicate/maplicate-editor , https://www.maplicate.xyz/
https://github.com/xuwaters/editor.sh , https://editor.sh/home
https://github.com/rudi-c/alchemy-book  , https://digitalfreepen.com/2017/10/06/simple-real-time-collaborative-text-editor.html

https://github.com/convergencelabs/monaco-collab-ext
https://github.com/munshkr/flok
https://github.com/P2Pvalue/jetpad
https://github.com/alabid/flylatex
https://github.com/stubailo/meteor-blocks
https://github.com/azat-co/editor
https://github.com/chaoscollective/Space_Editor
https://github.com/fiduswriter/fiduswriter
https://github.com/eberlitz/eb-editor

---

Found more VS Code extensions -

https://github.com/sockscode/sockscode-vscode
https://github.com/sockscode/sockscode-server
https://marketplace.visualstudio.com/items?itemName=shyykoserhiy.sockscode-vscode

https://marketplace.visualstudio.com/items?itemName=the-wire.rt-code-collab
https://github.com/THE-WIRE/RT-Code-Collab
https://github.com/THE-WIRE/web-rt

---

Thoughts on editing:
Only one or a few users can edit? Not all users. Hmm. Viewers/Editors concept.
Viewers can only view.

---

Looks like VS Code Live Share allows others to build on top of it? Check it
out!

https://marketplace.visualstudio.com/items?itemName=lostintangent.vsls-whiteboard
https://github.com/vsls-contrib/whiteboard

https://marketplace.visualstudio.com/items?itemName=lostintangent.vsls-pomodoro
https://github.com/vsls-contrib/pomodoro

---

More VS Code Live Share stuff! 

https://github.com/vsls-contrib
https://github.com/vsls-contrib/awesome-liveshare

---

Comments on Code and Code Review - 

https://marketplace.visualstudio.com/items?itemName=CodeStream.codestream
https://www.codestream.com/

---

Noticed something cool - recording and playing the process of programming

https://marketplace.visualstudio.com/items?itemName=wix.codio

Just something to check in case we are looking at tests or tutorials and
stuff. Collabortive tools are key for teachers and it can be interesting to
see how things came up to be. git can also help, but it can only jump from
one commit to another commit, not see at a more micro level ;)

---

Share project or file from VS Code with the world

https://marketplace.visualstudio.com/items?itemName=code-share.code-share

[Codesandbox](https://codesandbox.io) is used to share the code I think

---

Collaborate in VS Code with AWS Cloud9 service

https://marketplace.visualstudio.com/items?itemName=iann0036.live-share-for-aws-cloud9
https://github.com/iann0036/cloud9-sync

---

Another live share thing for VS Code

https://marketplace.visualstudio.com/items?itemName=DimaCrafter.vs-collab

---

unity collaborate UI? gotta check

https://marketplace.visualstudio.com/items?itemName=thainayu.vscodeunitycollab
https://github.com/Thaina/vscodeunitycollab

---

VS Code collaborative editing

https://marketplace.visualstudio.com/items?itemName=lyuboraykov.share
https://github.com/lyuboraykov/vscode-share

---

Holy god! Atom text editor has an open source way to collaborate!!! :D
Damn! That's it. I'll go contribute, and also try to port it to VS Code
may be? And Sublime and what not? :P Let's see :)

https://teletype.atom.io/
https://github.com/atom/teletype

Thanks to Martin Klepmann for mentioning about this feature in his talk
here https://www.youtube.com/watch?v=B5NULPSiOGw

https://github.com/atom/teletype-crdt
https://github.com/atom/teletype-server
https://github.com/atom/teletype-client

---

High Responsiveness for Group Editing CRDTs
https://pages.lip6.fr/Marc.Shapiro/papers/rgasplit-group2016-11.pdf

---

Different Sequence CRDTs

WOOT
Treedoc
RGA
RGASplit
RGA with Interleaving
Logoot
LSEQ
Astrong
LSEQSplit
LogootSplitAVL
Dotted LogootSplitAVL?

---

https://www.youtube.com/watch?v=M8-WFTjZoA0 so this talk tells how for text
docs automerge library may not help as automerge uses RGA Split algorithm -
need to check this and the speaker asks us to use something more efficient
and better, like Dotted LogootSplitAVL. 

---

Some research papers that are mentioned in [teletype-crdt](https://github.com/atom/teletype-crdt)
are 

Data consistency for P2P collaborative editing
https://dl.acm.org/doi/10.1145/1180875.1180916
https://dl.acm.org/doi/pdf/10.1145/1180875.1180916

Supporting String-Wise Operations and Selective Undo for Peer-to-Peer Group Editing
https://dl.acm.org/doi/10.1145/2660398.2660401

High Responsiveness for Group Editing CRDTs - I had mentioned it before too.
https://dl.acm.org/doi/10.1145/2957276.2957300

Looks like I got tons of research papers to checkout!

I need to understand the algorithm that [teletype-crdt](https://github.com/atom/teletype-crdt)
uses.

---

Tasks:
1. Read the papers

Data consistency for P2P collaborative editing
https://dl.acm.org/doi/10.1145/1180875.1180916
https://dl.acm.org/doi/pdf/10.1145/1180875.1180916

Supporting String-Wise Operations and Selective Undo for Peer-to-Peer Group Editing
https://dl.acm.org/doi/10.1145/2660398.2660401

High Responsiveness for Group Editing CRDTs - I had mentioned it before too.
https://dl.acm.org/doi/10.1145/2957276.2957300

While reading, make notes of everything you learn. Use
diagrams, etc. This will be useful to read again and also
to present it to the papers we love community! :)

2. Find out the algorithm used by automerge
3. Find out the algorithm used by teletype-crdt

---

WOOT
https://github.com/siuying/woot-doc
https://github.com/t-mullen/woot-crdt
https://github.com/t-mullen/logoot-crdt
https://github.com/d6y/wootjs
https://github.com/alexandrepiveteau/distributed-kotlin
https://github.com/ansonl/objc-woot
https://github.com/kana-sama/edita
https://github.com/disordinary/ed

---

https://github.com/alexandrepiveteau/elm-ordt

https://github.com/search?q=crdt

https://github.com/ipfs/notes
https://github.com/ipfs/notes/tree/master/CRDT

https://github.com/neurodrone/crdt

https://github.com/asonge/loom

---

https://github.com/coast-team/dotted-logootsplit

https://github.com/automerge/automerge/blob/master/INTERNALS.md

https://sci-hub.tw/

---

https://duckduckgo.com/?t=ffab&q=atom+editor+collaboration&ia=web

---

https://dl.acm.org/doi/10.1145/1180875.1180916
https://dl.acm.org/doi/10.1145/3133933
https://dl.acm.org/doi/10.1109/3PGCIC.2012.26

https://dl.acm.org/action/doSearch?AllField=crdt

---

Okay, I'm done reading the implementation of

Data consistency for P2P collaborative editing
https://dl.acm.org/doi/10.1145/1180875.1180916

I didn't read the proof part of it though. Might have to glance through that
once. I was planning to implement WOOT and understand it better and even use
it build a real world app like a collaborative editor. 

I was checking the Ace editor. It was good to check some of it's features.
It gave features to listen to events which gave a delta - insert/remove.
I think I'll get back to that.

I also though about how to propagate the operations among all the peers.
Since it's a broadcast, I thought it might be too much for one peer to
send all it's operations to all the other peers. If it's a P2P network,
why can't it just send to some of them and then that can be propagated
to the other peers. 

I was thinking about checking out some protocol like serf - and probably
implement it in js or something to use for web apps. But that's too much.
Also, there might be existing solutions - for example https://libp2p.io .
Also, there are other broadcast mechanisms and implementations out there,
and not just these. Anyways, I'm planning to read the next paper now. Which is

Supporting String-Wise Operations and Selective Undo for Peer-to-Peer Group Editing
https://dl.acm.org/doi/10.1145/2660398.2660401

---

RGAs - Replicated abstract data types: Building blocks for collaborative applications
RGAs-replicated-abstract-data-types-building-blocks-for-collaborative-applications
http://csl.skku.edu/papers/jpdc11.pdf

Optimistic Operations for Replicated Abstract Data Types
optimistic-operations-for-replicated-abstract-data-types.pdf
https://cs.kaist.ac.kr/upload_files/report/1254967150.pdf

Convergent and Commutative Replicated Data Types
convergent-and-commutative-replicated-data-types.pdf
https://core.ac.uk/download/pdf/55634119.pdf

Replicated Data Types
replicated-data-types.pdf
https://hal.archives-ouvertes.fr/hal-01578910/file/replicated-data-types-Encyclopedia-DB-systems-2016-authorversion.pdf


LogootSplit Sequence CRDT
Supporting Adaptable Granularity of Changes for Massive-scale Collaborative Editing
supporting-adaptable-granularity-of-changes-for-massive-scale-collaborative-editing.pdf
https://doi.org/10.4108/icst.collaboratecom.2013.254123
https://eudl.eu/doi/10.4108/icst.collaboratecom.2013.254123
https://www.researchgate.net/publication/269071934_Supporting_Adaptable_Granularity_of_Changes_for_Massive-scale_Collaborative_Editing

Delta State Replicated Data Types
delta-state-replicated-data-types.pdf
https://arxiv.org/pdf/1603.01529.pdf

A comprehensive study of Convergent and Commutative Replicated Data Types
a-comprehensive-study-of-convergent-and-commutative-replicated-data-types.pdf
https://www.researchgate.net/publication/50949847_A_comprehensive_study_of_Convergent_and_Commutative_Replicated_Data_Types

---

Tutorial: How to build an Collaborative Editing Application with IPFS using CRDT
https://www.youtube.com/watch?v=-kdx8rJd8rQ

How to make a real-time collaborative text  editor in 5 easy steps! // Rudi Chen
https://www.youtube.com/watch?v=jIR0Ngov7vo

My own playlist: Real Time Collaborative editing
https://www.youtube.com/playlist?list=PL6xKBQ9SsrsafblRImhUwe7hydsqMzI3y

---

I found this thing called Yjs, and a research paper for "YATA" and that Yjs is
an implementation of YATA. Details below -

YATA

https://www.researchgate.net/publication/310212186_Near_Real-Time_Peer-to-Peer_Shared_Editing_on_Extensible_Data_Types

https://github.com/yjs/yjs

http://y-js.org/

https://yjs.dev/

https://discuss.yjs.dev/

https://gitter.im/Yjs/community

https://github.com/yjs/yjs-demos

https://github.com/yjs/y-webrtc

https://yjs.dev/#features

The demo was done using these editors -
ProseMirror - rich text editor
Quill - rich text editor
Drawing (there was some collaborative drawing thing)

https://github.com/yjs/yjs/blob/master/README.md

https://yjs.dev/#community

https://github.com/dmonad/crdt-benchmarks

https://www.tag1consulting.com/blog/deep-dive-real-time-collaborative-editing-solutions-tagteamtalk-001-0

https://publishpress.com/blog/yjs/

https://www.tag1consulting.com/blog/yjs-webrtc-part-1

http://results.learning-layers.eu/infrastructure/client-frameworks/yjs/

---

About gossip protocols for networking - 

https://www.cs.cornell.edu/projects/Quicksilver/public_pdfs/SWIM.pdf

https://www.serf.io/docs/internals/gossip.html


---

“Collaborative text editing with Logoot” by Ravern Koh https://link.medium.com/fi0wHOuax6

Logoot CRDT: interleaving of data on concurrent edits to the same spot?
https://stackoverflow.com/q/45722742/4772008


Logoot: A Scalable Optimistic Replication Algorithm for
Collaborative Editing on P2P Networks
https://hal.inria.fr/inria-00432368/document

Logoot-Undo: Distributed Collaborative Editing System on P2P Networks
https://www.researchgate.net/publication/47441669_Logoot-Undo_Distributed_Collaborative_Editing_System_on_P2P_Networks

"There are several CRDT algorithms (LSEQ, Logoot, WOOT, Treedoc)..."
https://news.ycombinator.com/item?id=12304305


Collaborative text editor using Logoot CRDT algorithm 
https://github.com/mkdynamic/logoot


LSEQ: an Adaptive Structure for Sequences in
Distributed Collaborative Editing
https://hal.archives-ouvertes.fr/hal-00921633/document

Logoot: a P2P collaborative editing system
https://hal.inria.fr/inria-00336191v3/document

Supporting Adaptable Granularity of Changes for
Massive-scale Collaborative Editing
https://hal.inria.fr/hal-00903813/document


A String-Wise CRDT for Group Editing
https://dl.acm.org/doi/10.1145/2389176.2389198
https://dl.acm.org/doi/pdf/10.1145/2389176.2389198

Evaluating CRDTs for Real-time Document Editing
https://hal.inria.fr/inria-00629503/document

A Comprehensive study of Convergent and Commutative Replicated Data Types
https://blog.acolyer.org/2015/03/18/a-comprehensive-study-of-convergent-and-commutative-replicated-data-types/

Xiao Lv
https://dblp.org/pers/l/Lv:Xiao.html

https://www.quora.com/How-do-I-download-IEEE-papers-for-free?top_ans=161094348

https://sci-hub.tw/

---


