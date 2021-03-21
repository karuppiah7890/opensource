# Browser Stack Clone

I have heard about Browser Stack as a company before

I was continuing to think about implementing Browser Stack! :)

Yeah, I'm pretty ambitious, lol

So, yeah, Open Source version of all features of Browser Stack, hmm?

I was checking what features it has. It has too many. Haha

Browser testing related products, mobile app testing related products, selenium
related products too. Hmm

Browsers, mobiles - there's a lot of combination in it.

Browser - Firefox, Safari, Opera, Chrome. All different versions.
Mobiles - Too many manufacturers like Apple, Google, Mi, Nokia etc. Too many
models. Hmm
Operating systems - Linux distributions, windows, mac, Android, iOS. All
different versions.

---

YouTube Channel - https://www.youtube.com/channel/UC19qZKD_y-1pCPS5ZJWtlsA

Quick Overview - https://www.youtube.com/watch?v=N0olBr8n5zE

Demo Search - https://www.youtube.com/results?search_query=browserstack+demo

One Demo - https://www.youtube.com/watch?v=ATLrjWmHPxM

---

One of their USP - Unique Selling Point seems to be running tests on real
devices, hmm

Actually, cross browser testing is something that some people don't even wanna
do. They prefer letting the browsers take care of keeping up with standards
instead. I remember seeing a blog post about how cross browser testing is a bad
idea. Let me go get that blog post first

This is the one

https://medium.com/@you54f/reading-time-10-mins-8b6e7ef90062

---

Some notes from the past in my notes app -

This is about automated testing of web apps in browsers and mobile apps in emulators and simulators.

What test is run though? As in, who writes the test? And what's the input to this platform? Test code?

Browsers - there are many of them. Firefox, Chrome, Safari, Internet Explorer, Opera. And there are different editions for these browsers, for example - Firefox Focus, Firefox Developer Edition. And all of these browsers also have multiple versions. And there are lot more browsers - some of the recent ones that I heard are - Brave, Beaker. Of course there are tons more, old and new ones. And many of these browsers are also supported for different platforms and devices. Platforms / OSes - Android, iOS, Windows, Linux, MacOS. Devices - Desktop, Tablet, Phones, TV.

When the tests are run, for example, say, using Taiko, what do people expect from these tests. A test can pass or fail, right? What about some weird or unexpected error occurs? Like null pointer exception, finally it will be a failure, but different kind of test failure, as in, the test failed to run in the first place, it has to run properly to say if the test passed or failed as expected and actual output was different. And would people expect to take screenshots or snapshots of browsers? Hmm.

Building the platform - headless browsers vs browsers with GUIs? How to run? VMs, containers? For both, we need some form of orchestration and be able to horizontally scale up and down, so that resources are not wasted. Ideally containers, for example docker with some container orchestration like Nomad and Hashicorp ecosystem could be used or Kubernetes which is all batteries included.

And the browsers, are we running them only on Linux and testing? Or going to help with testing the web app in browser for different platforms and devices. What browsers (including browser edition) and what versions to support?

Check what is Selenium, Appium, Selenium Grid etc.

---

Some more notes -

Kubernetes. Or Nomad.

Create custom resources. Which has information on what jobs to run - Different browsers and platforms. Parallelization level depending on the user's pricing plan. Accordingly run multiple jobs in parallel at once using Kubernetes jobs. If one of the jobs finishes, then start the other. Typical parallelization problem with some level of parallelization. Maybe many have solved this problem already. For example, faktory which runs jobs - same company as the one behind sidekiq background job library which has OSS version and enterprise too

Or celery
Or closed source AWS Lamba. But costly and will need docker runtime. Docker runtime is easy!!

On premise vs cloud? Support both!!

---

Some more stuff that can be used to run the workloads on Kubernetes -
Tekton and similar CRD based tools. ArgoCD?

Nomad has good support for Windows I think and probably Mac too. I don't know
about Kubernetes though, I mean I have seen there's some support, but I don't
know how much. Linux is the main platform for containers and containerization,
not sure how they would run for Windows and Mac. Hmm

---

In one of the videos I noticed that a user can get access to a real system's
browser. The system can have any operating system and any browser (any
version) installed in it based upon the user's choice

https://www.google.com/search?q=remote+desktop+research+papers&oq=remote+desktop+research+papers

https://scholar.google.co.in/scholar?q=remote+desktop+research+papers&hl=en&as_sdt=0&as_vis=1&oi=scholart

https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0207512

Remote Desktop Protocols

https://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software

https://en.wikipedia.org/wiki/Chrome_Remote_Desktop

https://en.wikipedia.org/wiki/Chrome_OS#Remote_application_access_and_virtual_desktop_access

http://cord.sourceforge.net/

https://www.xtontech.com/blog/rdp-vs-vnc-access/

https://en.wikipedia.org/wiki/SSH_(Secure_Shell) and https://en.wikipedia.org/wiki/X_Window_System

---

Remmina:

https://en.wikipedia.org/wiki/Remmina

https://gitlab.com/Remmina/Remmina

https://remmina.org/

https://remmina.org/how-to-install-remmina/

https://gitlab.com/Remmina/Remmina/-/wikis/Home

---

https://github.com/search?utf8=%E2%9C%93&q=remote%20desktop%20rust

https://github.com/citronneur/rdp-rs

https://github.com/citronneur/rdpy

https://github.com/citronneur/node-rdpjs

---

https://github.com/rustdesk/rustdesk (closed source)

https://rustdesk.com/ (closed)

https://github.com/rustdesk/rustdesk-server (closed)

---

https://github.com/Devolutions/IronRDP

---

https://github.com/search?q=remote+desktop+protocol

https://github.com/FreeRDP/FreeRDP

https://www.freerdp.com/

https://github.com/cedrozor/myrtille

https://en.wikipedia.org/wiki/Xpra

https://en.wikipedia.org/wiki/UltraVNC

---

https://www.google.com/search?q=remote+desktop+protocols+comparison&oq=remote+desktop+protocols+

---

https://www.google.com/search?q=remote+desktop+protocol+research+papers&oq=remote+desktop+protocol+research+papers

https://www.irjet.net/archives/V7/i4/IRJET-V7I4982.pdf

https://www.researchgate.net/publication/4105113_Research_and_implementation_of_remote_desktop_protocol_service_over_SSL_VPN

---

Browserstack features

https://www.youtube.com/watch?v=Vb2u2EUSa1o

https://www.browserstack.com/automate

https://www.browserstack.com/automate/features

Running Selenium tests on real devices, hmm

Running selenium tests from local on the Selenium grid that Browserstack owns.

---

https://github.com/search?utf8=%E2%9C%93&q=appium

https://github.com/appium/appium

https://github.com/AppiumTestDistribution/AppiumTestDistribution

---


Browserstack clones and related projects

https://github.com/search?utf8=%E2%9C%93&q=browser%20stack%20clone

https://github.com/search?q=browserstack+clone

https://github.com/hernan604/BrowserStack-Clone

https://github.com/search?q=browserstack

https://github.com/browserstack

---


