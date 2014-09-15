# Learnings

Very explicit style.

_ meaning 'don't care'. FOR loop indexes. Variables only used to check if casting works.
defer() for closing resources and catching panics.
Panic as clearly not for control flow.
Create methods by pinning a function to a type.
Inheritance using explicit embedded type.

go to run any func in a thread.
Channels with left operator <-
chan myChan - without buffer size - is a blocking semaphore (write blocks until read is ready) for a given type.
chan myChan with buffer size is a typed queue.
chan myChan can be cast as read/write or <-RO or WO<-

select reads from whichever channel is ready - a switch() for chans.
time.After creates a channel and waits N seconds before sending the time.
You can select on the time chan to act after a timeout.
Includes default:

Capitalised functions are exported as public, lowercase are package private.

Built-in testing. Begin function with TestFoo(bar *testing.T)

# Article

## I hate the golang article

It gets too clever too quickly and assumes you are using the github magic. Wait, how does simple local stuff work?
I want to learn one thing at a time, not start messing with github repos.

## The conventions

A workspace has three non-negotiable directories:
bin - executables
pkg - library binaries (*.so). Organised by architecture, e.g. linux_amd64.
src

## Split 3rd party and yours

Go is fancy and will download stuff.

Ah like npm (JavaScript) or Maven (Java)! Kind of. Except there is no nicely segregated download repo - e.g. node_modules or ${home}/.m2/repository. By default everything gets chucked in the same workspace.

So we need two workspaces.

The idea of 3rd party and my comes from http://blog.tideland.biz/2013-07-09-go-environment-setup

## So where do I git clone?

Into $GO/my/src/github.com/your_id

## GOPATH

The command go get will install the sources and the compiled package into the *first* directory of the path.
