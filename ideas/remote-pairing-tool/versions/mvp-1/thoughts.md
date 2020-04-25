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

