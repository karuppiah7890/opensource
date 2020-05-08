# licensing

If I'm going to create software (client side or server side), and if it's going
to be paid software, at some point I need to think about how to handle licensing
and only allow people who paid to be able to use the software and also allow
free trials

I only thought this whole thing in terms of server software. Need to see what's
different for client software and need to see if we need more thought on that.

# Related stuff

I think these are all related - Licensing, Distribution, Free Trial strategies
Just my thought 😅

# Server Software Licensing

First of all, I'm thinking about this because the idea is that - I'll give the
server software to customers so that they can self host it - why? because
some customers (or many) care about data and don't want to use the SaaS offering
and instead want to self host in their servers / machines / data centers, which
could be in a public cloud or private cloud or just a bunch of VMs in their
office or something. For this the software has to be very simple to run and
manage, that's a whole thing by itself. Here we will think only about how to
do licensing

## The user flow

User wants to self host my software. So, how does that work? First, they need to
get the software. So, I need to distribute the software, again, a whole thing by
itself. Unfortunately it's a bit tied up with this I think? Or may be it should
not be? Let's see. So, my software can be roughly distributed in two ways

1. Completely publicly - anyone can download the software

Anyone as in, they don't need to do anything, no credit card, no signup, nothing.
This is too open. I think I might not choose this, for various reasons. But,
let's see. But, this means that the software still has to stop working if the
license expires.

2. Privately - only certain set of people can download the software

Certain people as in, people who signed up and gave credit card. Or just signed
up. This seems like a more probable thing that I'll choose

## Solutions

Below are some of the most basic solutions I had for making sure the server software
runs only for the stipulated / expected time -

### Free trial users

If I want a free trial server software to stop working after some hours or
days, I need to be able to detect this. For example, let's say there's no
concept of license key or anything of that sort. The only thing that the user
has is the server software binary (let's assume there's just one binary). Now,
the user runs it. How do I make sure that it stops after some time? As it's a
free trial user.

0. The teeny tiny idea that I had initially was to store some data in a file,
and then use that file as reference to know when to stop. More like the file was
a DB for the server. I can write to some file when the server starts. It could
be some secret file that the user cannot find?

Problems:
- It's very possible that the user can find the file and delete it, so, now
the server will keep running forever, and if the file is again written, user
will again delete it as the user knows about it
- The user can simply run the server in different machines and it will still
work, as every time a new machine is used, a new file will be created. But yeah,
it can be tedious for the user in this case, where they need to keep running
it in a new machine - as it's a server and servers should ideally keep running,
so they need load balancer and stuff and make sure it's just up always, but if
they find about the file, it's like a bonus for them, delete file, run multiple
instances too and have fun 😆

1. The most basic solution I had was, when building the binary, embed a time
inside the code - time for expiry, or time of binary creation. Some reference
time, and of course with timezone, preferrably UTC, which is common. So, now the
code has details on a reference on when it needs to stop. When the server starts,
it can check the system time and stop if the trial has expired. If it has not
expired, then it can keep running, and there can be a background process or thing
in the code, which can check the system time every few minutes - like 5 minutes
or 10 minutes and then kill the whole server if the time has expired

Problems with this solution: The user can possibly find out that the server
is using some kind of system time and so they can gimmick the server by changing
the system time - of course it could have possible issues with the way the server
runs if it depends on the system time for anything. But other than that, no problems
to run the server. This way they could possibly run the server for a very long
time

2. To over come the problems in solution 1, I thought, why not use some
public server to check time and not depend on system time? This way, I can know
the exact correct time and stop the server running properly

Problems:
- Some people have airtight machines. They explicitly put firewalls and rules to
allow any network communication. So, it's very possible that our server might not
be able to contact the public server for checking time. So even if the user is
legitimate, we might stop the server, saying it has expired - as we don't want
to explicitly say we were trying to check time from a public server and couldn't
and hence declared the time as expired. Declaring internal working information
can help the user to gimmick the system, if that's possible
- People can also possibly find out what network communications are being done
by the server. This way, they could find out about the public server. They could
then gimmick the public server - as it's public, they can find out what API
response it gives and then they can run one locally, spoof the DNS, and even if
it's HTTPS, they can create a self signed certificate and make their certificate
as trusted in the sytem. It's possible, I have seen. So, I think it's completely
possible to gimmick the system, by running a spoof public server themselves

3. One way to solve the problems in solution 2 is - making sure that the HTTPS
certificate check is more better - like may be consider embedding the CA
certificate of the public server's CA in the binary and using that and not
trusting the system. I think browsers come with embedded CA certificates, that's
what I have heard. Need to check. So, may be if we do a better job in checking
the HTTPS certificate and make sure spoofing / tricking the system is surely not
possibly, then we can possibly stop the server at the correct time for a trial
user

Problems with all the above 3 solutions:
- Has no provision to support paid users. Talks only about trial users and about
fixed expiry time for them. Ideally expiry time is flexible - if a trial user
suddenly pays within the trial and converts to a paid user, the server should
NOT stop and instead the expiry time moves away based on the payment. So, that
was the case of trial user to paid user migration. Also, for direct paid users,
there is no concept of fixed expiry. Same stuff. Flexible expiry based on
payment.

Also, we should not abruptly stop the servers even if payment was delayed. We
should first start sending payment alerts before hand, like long before the
last date for payment. And based on subscription or whatever kind of pricing
we have, we have to consider when to really stop the server, even if payment
was delayed, like payment date has passed. This is because server software is
key, and needs to keep running. If user could not pay, we need to check with
user and see what's happening, before being brutal 😅

### Copy Cats!

There's one problem with software or any digital thing. Usually it can be copy
pasted. Right? For example, let's say I buy an ebook from some platform and
they gave me the PDF, MOBI and other versions of the ebook, so that I could
download it. What are the problems here? I can easily take this, and give it
to my friends through flash drives, or any storage, and through the Internet,
in dropbox, drive or any file hosting platform, and actually distribute to
any number of people - the limit is the whole world. No wonder people don't
allow you to download paid content into your computer, phone, tablet or any
system's files, and instead allow you to only download into their platform.
For example, for Kindle Ebooks, the ebooks are only available through Kindle
app - which has download options inside it, and offline reading options, and
yeah, they need to make sure that they store the ebook securely in the system's
files so that no one can sneak into it and copy it. Same for Netflix videos,
Amazon Prime videos and whatever paid services are out there. And even when
the video service platforms stream the video to you, they make sure you can't
download it if it's paid or if their platform prohibits it - Netflix, YouTube,
Amazon Prime. In fact Netflix and other on demand video streaming services
use some tech called Digital Rights Management (DRM) I think. Anyways, all this
to make sure people just can't simply copy paste and distribute content -
then the companies will be at loss - as one user will pay and tons of users
will consume the content. This issue has to be tackled in my case too.

If I give my software to someone and give them a license to run it, they could
just give that license to everybody in the world and everyone will be sharing
a single license. Now, let's compare it to Netflix. Netflix has pricing plans,
one of them says that a maximum of 4 users can use the account. So, you would
think that only 4 users can login, to their 4 devices. But actually, people may
have multiple devices, phone, laptop, desktop, tablet, what not. So, they can
login from any device and use the app or the site in the browser. What Netflix
actually caps is - the number of users who can stream simultaneously - that is
4 in this case. So, how many ever devices these 4 people have, they can only
stream simultaneously on 4 devices, or actually, 4 screens. Like, one can't even
stream two things simultaneously in different tabs of the same browser. But yes,
I guess if you use incognito tab or a separate browser, you can stream, but that
would be considered as one more screen. So, it's more at screen level - how many
things are being streamed. Of course, if this is the case, someone can get a
Netflix account and share it with not just 4 people, but may be more. Like,
people from different timezones - they could make sure that at any time, only
4 are watching, and others have something else to do. Have some schedules to
coordinate and what not, and it will be like the perfect planned way to use
Netflix almost 24x7 by multiple people, that is more than 4, with just a single
account. Based on what the plan says, it's possible, yes. But hey, Netflix is
not some fool, right? It will be a loss for their business if this happens. Of
course they are going to allow only 4 simultaneous screen streaming at a time,
that does not mean tons of users can use it. It's a family plan, so, I think
they will have some max number of devices for usage, and I believe they might
also be doing some fraud detection - password hacks and also the cases I
mentioned - too many people (like, above some threshold) using the same account,
which is suspicious and not good for business like I said above - I guess they
suspend such accounts? So yeah. That's the level of security and checks that
must be there. No malicious attacks by hackers and no malicious usage, more like
over usage by legitimate users.

So, even in my case, I need to check the license usage - if it's a single
user license, only single server can run with it, it's multi user, support that
too. And if the number of users goes more than the limit, they should not be
able to use it.

### Free Trial and Paid Users

This solution is kind of the one. Kind of inevitable. And most probably more
solutions will be based on top of this is my guess. This is considering the
fact that we need to solve the problems that were mentioned above.

Some random thoughts:

Heartbeat will be sent by servers (entities) to license server every t time.
Heartbeat with information to identify the machine or server uniquely and also
to identify the pricing plan given the license key and more details which
I don't know now

Concurrent connections or simultaneous connections - after every few minutes,
check how many alive servers are there. If there's more than some. Kick the ones
that came in later.

How to identify each server separately? Use UUID? At start. Store it in file or
something? Or have it in memory? Restarts will create new UUID

Gracefully leaving of license by server during graceful shutdown?

Crazy shutdown? It will be marked dead is it's heartbeat doesn't come

Failing of license check by license server should not stop server. Atleast some
fails can be forgiven, if it's license server side failure. Allow some 10
failures from license server side. Or all server side errors can be forgiven?
As it's our problem is license server is acting crazy.

What about real license issues? Not renewed licenses, trials. Allow 10 failures.
Let's give them a chance. Also, what if license server works but is misbehaving,
may be due to storage etc issues, like license info gone, then also valid
license issues will come as license server thinks all licenses are wrong.
Gotta be careful. Need to build resilient systems, and with backup too, of course.

And in my storage - I want to know everything that happened. Like when the
license was extended. And how it's renewed etc. Every detail in history of
licensing, subscription and payments


License server to give the UUIDs to the clients. This way no one hacks and finds
UUID and behaves as one. Actually. Whoever gives, imitation is still possible.
How to avoid that?? How can one even change the UUID? Oh yeah. I was going to
store the UUID. I think we can have it in memory itself. And consider it dead if
it doesn't report or if gracefully leaves. Client can stop reporting because the
network is down or the network is blocked. We need to tell users that the
network should be up. Or else, after a few failures, the client will not work.
And license will be considered invalid.

Now what if customer wants the client to run in an air tight manner? And they
still should be able to run during their license time. Hmm. I guess we can do
something like license key, that itself has information regarding when is the
expiry date and what not, but, it cannot be extended or flexible, as that would
need network connection to get information. So. If the requirement is for air
tight, they need go redeploy with new license key for updated expiry date. Or I
need to think of some other way. Let's see research papers for this

In the whole thing, we cannot allow anyone to know our license server's
API - the request body, response body. Everything has to be secure. No man in
the middle attacks. I think request URI is hard to hide. Hmm

https://www.license4j.com/documents/floating-license-server/

https://dzone.com/articles/opensource-license-manager

https://cryptolens.io/open-source/

https://github.com/furkansenharputlu/f-license

https://github.com/open-license-manager/open-license-manager

GitHub - license-management topic

http://www.diva-portal.org/smash/get/diva2:696982/FULLTEXT01

https://www.techsoup.org/support/articles-and-how-tos/introduction-to-microsoft-server-and-client-licensing

https://www.wibu.com/magazine/keynote-articles/article/detail/license-server-in-high-availability-environments.html

https://scholar.google.co.in/scholar?q=license+server+research+papers&hl=en&as_sdt=0&as_vis=1&oi=scholart

https://patents.google.com/patent/US5023907A/en

https://patents.google.com/patent/US6343280B2/en

https://patents.google.com/patent/US5579222A/en

https://patents.google.com/patent/US7996335B2/en

https://patents.google.com/patent/US7885896B2/en

https://patents.google.com/patent/US8732841B2/en

https://patents.google.com/patent/US20020138442A1/en

https://patents.google.com/patent/US20070011097A1/en

---

I need to read research papers on license servers and licensing systems.

---

disrtribution - single binary for everyone.
with all features. but features are unlocked
based on license and timing too - trial vs paid

or separate editions - enterprise edition,
community edition etc. community edition
could even be open source. more like
open core 🤷‍♂
