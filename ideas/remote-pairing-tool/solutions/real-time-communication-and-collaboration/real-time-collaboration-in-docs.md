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


