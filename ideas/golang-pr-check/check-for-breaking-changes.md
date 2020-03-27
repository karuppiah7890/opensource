# check-for-breaking-changes

A tool to check for breaking changes in the PR. This will augment the PR
review process by automating some stuff - so that this does not have to be
manually checked by folks when reviewing PRs!

If the project has multiple packages with several entities exported - methods,
functions, types, constants and what not, a Pull Request must not change it,
unless the Pull Request is for a breaking change - first PR for a major version
bump!

So, how does one check if a PR has made breaking changes. Manually, I would
check if the signature of exported methods have been changed by checking the
diff of the PR.

The tool could do something similar! This would be the smallest piece of info
to process to find this information - checking the diff alone

But if diff is hard, we can get the whole project - without PR and with PR,
and find all the exported entities and find the difference between the list for
the before PR and after PR code. But this is a lot of work for the program - to
get all the exported entities.

This would be a fun project to try out! :D

One thing to note is - apparently packages with internal in their name
cannot be imported by external packages. Links - 

http://stackoverflow.com/questions/41571946/ddg#41572137

https://docs.google.com/document/d/1e8kOo3r51b2BWtTs_1uADIA5djfXhPT36s6eHVRIvaU/edit#!

https://golang.org/doc/go1.4

https://golang.org/doc/go1.4#internalpackages

