# Mouse and Keyboard control from Mobile

This is NOT my idea. Some of my colleagues were trying to build an Open Source
tool for this. I loved the idea and wanted to put it out in case anyone wants
to try it out. I may or may not try it out.

So, the idea is like this - apparently there are some android apps to help you
with controling your desktop mouse. I'm not sure what's the use case.

So, the ideas for implementing this were

- Use existing libraries to interface with the desktop platform - something
  based on use case, or even cross platform libraries or software, instead of
  building from scratch. There are many such tools to help with controlling
  mouse and keyboard. And then build a server in the desktop, and then build an
  app. App communicates with the local server to control the desktop mouse and
  keyboard

- This is another awesome idea!! This based on the idea of bluetooth mouse and
  keyboard. Bluetooth mouse and keyboard work by connecting to the desktop or
  laptop through bluetooth. They send some data and desktop understands and does
  stuff. Similarly, mobiles have BLE - bluetooth. They can just connect to the
  computer (desktop or laptop) and be able to control the keyboard or mouse just
  like a bluetooth mouse or bluetooth keyboard, by imitating them!! :D This way,
  the user does NOT have to install anything in the computer, just connect with
  the bluetooth and it just works! :)

  Note: If the desktop does not have bluetooth, you need to
  use some bluetooth receivers to have bluetooth capabilities - some sort of
  USB kind of devices are present to help with this, you just plug it in and you
  now have bluetooth capabilities! :)

Links to existing Android Apps:
https://play.google.com/store/apps/details?id=io.appground.blek
https://play.google.com/store/apps/details?id=io.appground.blekpremium
https://play.google.com/store/apps/details?id=io.appground.gamepad - Game pad
