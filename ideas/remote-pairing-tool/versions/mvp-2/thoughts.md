I think the first thing to do is - do a spike on how to create a VS Code
extension

And then the next thing to do is - see if the project file structure information
can be obtained and if yes, how to obtain it

And then the next thing to do is - see how to modify the sidebar to show
project structure or anything, even though the computer does not have that
in it's local system - as that would be the case for the other user who would
be trying to access another user's system to see the project file structure

Each one of these would be a spike I think

And then I gotta see how to publish it in the marketplace - as that's how
extensions are distributed, so yeah

And also put some license key like stuff so that not everyone can use it!
May be put some TOTP based password? Or for now, just some random password.
Gotta see :) How to do it and if it's needed. Again. Spike ;) 

And then finally put it all together and that's it ;) I guess it's just a
bunch of spikes put together to make an MVP 🤣

So, I was checking what I can do to replicate the folder structure
from one VS Code to another VS Code. And probably some things for
the future too. Since the next steps is real time collaboration -
I was looking at solutions that support this - especially in a
decentralized manner. Some links -

https://gun.js.org/
https://github.com/amark/gun
https://gun.eco/docs/Introduction
https://gun.eco/docs

https://gun.eco/think.html
https://gun.eco/converse.html


So, with GunDB, the idea is to have a decentralized, offline first, distributed,
peer to peer DB. And it uses CRDT algorithm - Conflict-free Replicated Data
Type, to manage conflicts. I need to learn more on that. It seems promising.
Also, I'm only planning to support 2 users to start with, and they claim to be
able to support multiple users. And even though it's peer to peer, they
recommend having one or more relay peers, which is running as extra peers - more
like some centralized servers? so that if all peers (users) go down, the relay
peers can still hold all the data. Also, apparently not all users will have
all the data, but I think relay peers are supposed to have all the data, to
make sure there's someone who knows everything in case others go down, so that
data is not lost. Something like that. I need to read more upon how the peers
and relay peers work.

Other solutions I came across when searching for CRDT databases was these - 

https://github.com/orbitdb/orbit-db - It's based on something called IPFS, need
to check what that is

https://github.com/ssbc/ssb-db
https://github.com/kappa-db/kappa-core
https://github.com/johnny-morrice/godless
https://github.com/arso-project/kappa-record-db
https://github.com/AntidoteDB/antidote , https://www.antidotedb.eu/

