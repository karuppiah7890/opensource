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

---

Currently trying to create a standalone nodejs client similar to the golang
client for the swift grpc server.

Trying out the code here

https://grpc.io/docs/tutorials/basic/node/#loading-service-descriptors-from-proto-files

When I installed stuff using `npm`, got some security issues. Can't have
security issues in my app 😅 so, checking it out. I did this

```
$ npm i -S grpc @grpc/proto-loader
```

Got errors regarding `minimist` package security vulnerability. And I tried
the automated fix

```
$ npm audit fix
npm WARN controller-demo-nodejs-client@0.1.0 No description
npm WARN controller-demo-nodejs-client@0.1.0 No repository field.

up to date in 0.514s
fixed 0 of 3 vulnerabilities in 172 scanned packages
  3 vulnerabilities required manual review and could not be updated
```

Manual review was needed.

```
$ npm audit

                       === npm audit security report ===

┌──────────────────────────────────────────────────────────────────────────────┐
│                                Manual Review                                 │
│            Some vulnerabilities require your attention to resolve            │
│                                                                              │
│         Visit https://go.npm.me/audit-guide for additional guidance          │
└──────────────────────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > mkdirp > minimist                      │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > tar > mkdirp > minimist                │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Prototype Pollution                                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ minimist                                                     │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Patched in    │ >=0.2.1 <1.0.0 || >=1.2.3                                    │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ grpc                                                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ grpc > node-pre-gyp > rc > minimist                          │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://npmjs.com/advisories/1179                            │
└───────────────┴──────────────────────────────────────────────────────────────┘
found 3 low severity vulnerabilities in 172 scanned packages
  3 vulnerabilities require manual review. See the full report for details.
```

So, now I checked all these links

https://www.npmjs.com/advisories/1179

https://github.com/substack/minimist/commit/4cf1354839cb972e38496d35e12f806eea92c11f#diff-a1e0ee62c91705696ddb71aa30ad4f95
https://github.com/substack/minimist/commit/63e7ed05aa4b1889ec2f3b196426db4500cbda94

I need to understand the security vulnerability, for now trying to get rid of it

https://github.com/substack/minimist/commit/4cf1354839cb972e38496d35e12f806eea92c11f#commitcomment-38002136

https://github.com/maxogden/extract-zip/issues/86#issuecomment-602133618

https://www.npmjs.com/package/npm-force-resolutions

https://stackoverflow.com/a/60795003/1611925 or
https://stackoverflow.com/questions/58065817/npm-force-package-lock-to-update-a-sub-dependency-package/60795003#60795003

https://stackoverflow.com/a/60794976/1611925 or
https://stackoverflow.com/questions/53262690/force-npm-to-update-dependency/60794976#60794976

```
$ npm ls minimist
controller-demo-nodejs-client@0.1.0 /Users/karuppiahn/oss/github.com/karuppiah7890/controller-demo-nodejs-client
└─┬ grpc@1.24.2
  └─┬ node-pre-gyp@0.14.0
    ├─┬ mkdirp@0.5.1
    │ └── minimist@0.0.8
    └─┬ rc@1.2.8
      └── minimist@1.2.0
```

I'm just going to force everything to use `minimist@1.2.5` which is the latest

https://github.com/substack/minimist/releases

Hopefully no breaking changes 🤔 as `mkdirp@0.5.1` is using `0.0.8` version of `minimist`.
Let me check if they have actually upgraded. Okay, the latest version of
`mkdirp` is `1.0.4` https://www.npmjs.com/package/mkdirp?activeTab=versions , https://github.com/isaacs/node-mkdirp/releases

Actually, I could just lock the version for `mkdirp` and `rc`. Hmm 🤔

Wow. So, I tried different stuff. In between I realized `resolutions` is a
feature provided by `yarn` package manager 

https://classic.yarnpkg.com/en/docs/selective-version-resolutions/

Finally, I just got rid of `package-lock.json` and added it to `.gitignore`
and started using `yarn`. Surprsingly no audit issues this time. No vulnerabilities.
I got rid of the `resolutions` field in my `package.json` too!

Back to coding! Damn :P Spent too much time on that security issue.

Now, I'm trying to see how to load multiple proto files. In the code I see
this

```
/**
 * Load a .proto file with the specified options.
 * @param filename One or multiple file paths to load. Can be an absolute path
 *     or relative to an include path.
 * @param options.keepCase Preserve field names. The default is to change them
 *     to camel case.
 * @param options.longs The type that should be used to represent `long` values.
 *     Valid options are `Number` and `String`. Defaults to a `Long` object type
 *     from a library.
 * @param options.enums The type that should be used to represent `enum` values.
 *     The only valid option is `String`. Defaults to the numeric value.
 * @param options.bytes The type that should be used to represent `bytes`
 *     values. Valid options are `Array` and `String`. The default is to use
 *     `Buffer`.
 * @param options.defaults Set default values on output objects. Defaults to
 *     `false`.
 * @param options.arrays Set empty arrays for missing array values even if
 *     `defaults` is `false`. Defaults to `false`.
 * @param options.objects Set empty objects for missing object values even if
 *     `defaults` is `false`. Defaults to `false`.
 * @param options.oneofs Set virtual oneof properties to the present field's
 *     name
 * @param options.includeDirs Paths to search for imported `.proto` files.
 */
export declare function load(filename: string | string[], options?: Options): Promise<PackageDefinition>;
export declare function loadSync(filename: string | string[], options?: Options): PackageDefinition;
```

Not sure how to pass multiple file paths in a single string. 🤔But there's this
option called `includeDirs`. I could use that so that imports don't have
problems. Okay then. There's a way to load proto files with `import` statements

From the swift repo, I had to copy proto files

```
$  cp controller-demo/protos/*proto ../controller-demo-nodejs-client/protos/
```

I gotta see how to have it in a central place and keep it updated too 🤔 Hmm.
Not sure if mono repos can help. Quite possible :D Let's see. For now, copy
paste is fine. I guess 🙈

I used this to understand the keys inside the object

```
 console.log(Object.keys(protoDescriptor))
```

Wow. I was able to write the code and connect to it and move the mouse too
by contacting the swift grpc server!!! :D :D :D 

