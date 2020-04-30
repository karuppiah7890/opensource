# thoughts

* For the two users to connect to each other - use plain IP address and port
number. See if the two users can connect to each other. If not, use something
like https://ngrok.com for now! 

* See if you can use gRPC client and server for the networking component. Easier
for code generation! We don't have to write too much client side code then -
connecting, serializing, deserializing data and all. And I think it's efficient
compared to HTTP, so 🤷‍♂

* Use golang for networking component!

* Write controller component code in Swift for now to move the mouse. Look
out for libraries and the https://github.com/BlueM/cliclick objective-c
code

* Check how to make the networking component and the controller component
talk to each other. More like inter process communication. We can do
gRPC again? In Swift code too. To start with. Let's see.

---

Assumptions: The relative position / movement of a mouse can be captured.

UI -> imagine a blank window program. If the user clicks on it, the mouse
disappears, but the program starts to capture the movement / position of the mouse.
And the movements are sent to the other user's computer. Now - are we sending
absolute position or relative position (movement) of the mouse?

If we are sending absolute position, it means the position from first user's
computer is taken up and the mouse is moved to exactly the same position
in the other user's computer. What are the pros and cons to that? If there are
resolution differences, then we will have to do a mapping of the screen and
accordingly change the position by scaling up or down and then controlling
the mouse. 

Assumptions: the mouse movement can and will be captured beyond the window's
limits.

If we are sending relative positions, more like movements, what's the speed
of the movement of the mouse? At OS level you can set how fast you want the
mouse to move. So, does that affect things here? 

Okay, it's clear that I don't know anything about mouses and the above is just
some random logic based thoughts. More like a layman thoughts. I need to do
some spikes to understand more about mouses! 

Spike 1: How does one capture the actions of a mouse and details of a mouse?
What's possible and what's not possible? Does one need a blank window to
capture a mouse? Can it be done with no windows? That is, no GUI, at all.
What are the limits to capturing the mouse's actions? When can we do it and
when can't we? As usual explore a lot to checkout the unknown unknowns.

Check [spike thoughts](./spikes/spike1/thoughts.md)
---

After the above spike, I have a lot of code already ready. Now, I'm just
trying to modify the electron app so that it can contact the swift server
and is able to move the mouse. Then I'll try it with my friend may be, over
the Internet

