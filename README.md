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

Go makes some pretty strong demands on how you organise things. You're not going to have a flat structure with a ton of project directories, and a repository off to the side somewhere. In Go everything - source and binaries - lives in a single tree called a workspace.

A workspace has three non-negotiable directories:
bin - executables
pkg - library binaries (*.so). Organised by architecture, e.g. linux_amd64.
src

## Packages

A package is just a string. Slashes are important - they map to directories, just like the dots in a Java package name.

The Go tool has magic for certain package strings and can fetch from them.

You need something unique for your stuff.
Uniqueness. In Javaland the namespace went backwards, a very ISO sortable sort of scheme, so com.github and com.oracle would appear next to one another. Go prefers a more human-readable approach, so github.com.

The 'last part' - the part after the last slash - of the package name is important. This will match the directory with your stuff in it, and it's also the name of any executable produced.

1. Fully qualified package name (FQPN)
  - Used on the command line
  - Used in imports in source code
2. The executable name is taken from the last part of your FQPN. The github repo name. In my example `gotest`.
  - So the name of the source file doesn't matter, it could be `bananas.go`
3. 

## Split 3rd party and yours

Go is fancy and will download stuff.

Ah like npm (JavaScript) or Maven (Java)! Kind of. Except there is no nicely segregated download repo - e.g. node_modules or ${home}/.m2/repository. By default everything gets chucked in the same workspace.

So we need two workspaces.

The idea of 3rd party and my comes from http://blog.tideland.biz/2013-07-09-go-environment-setup

## So where do I git clone?

Into $GO/my/src/github.com/your_id

The formal name of your package (which itself can contain (an or N?) executable and N packages) is `github.com/your_id/gotest`.

## GOPATH

The command go get will install the sources and the compiled package into the *first* directory of the path.

## Doing stuff

By default the tools assume you're in your project (package/repo) directory. If you are anywhere else, use the fully qualified form so the tool can find it, `go install github.com/air/gotest`.

`go build` to compile.

`go install` to produce output artifacts: executables and libraries.

`go clean` doesn't do what you think. To have it actually clean build artifacts, you need `go clean -i`.

`go get` retrieves and builds the thing with any dependencies. `go get github.com/golang/example/hello` does not only a git clone and also an executable hello program. Nicely segregated from our code of course.

`go test` - built in testing! Yay.

`go fmt` - gets your code into standard form if you're into that sort of thing.


## Stuff

You can make files ignored with a _ prefix.

## But...

No versions are specified in dependencies. This is weird. You're always working with HEAD.
