---
title: "GopherCon Day 2"
date: 2017-07-17T21:00:01-05:00
author: "Cody Oss"
categories: ["conferences"]
tags: ["go", "gophercon"]
---

Like day one of GopherCon 2017, day two was full of awesome information! Here are some highlights from the
sessions I attended.

**NOTE**: You can view the official live blog of the con [here](https://about.sourcegraph.com/go/) for more detailed info.
Slide decks can he found [here](https://github.com/gophercon/2017-talks)

## Understanding Channels by Kavya Joshi
This was one of my favorite talks of the day. Kavya talked about how channels are implemented under the hood. Let me
tell ya, it is not how you think they are! She touches on some pretty cool optimizations the runtime makes. For example:
consider the case of a buffered channel that gets filled up. A goroutine then tries to put another item into the channel,
but it can't. It is another goroutine, the one that causes the channel to unblock again, that actually puts the next
item into the channel. This is because it can be done without having to yield the mutex to another goroutine, which ends
up being a nice performance boost! I highly recommend watching this talk once it is available.

## My Journey to Go by Ashley McNamara
This talk was one of those "feel good talks". Ashley brings up some great points through the talk. One of my favorite
quotes from the talk was: "Don't be to proud to accept help when it is offered". I think this is advice we can all
really take to heart.

## Advance Testing with Go by Mitchell Hashimoto
This was my second favorite talk of the day, and once it posts online I will need to re-watch it myself. Mitchell
covered many great points. I think the [official live blog](https://about.sourcegraph.com/go/advanced-testing-in-go-mitchell-hashimoto)
can tell it better than I though, so I will leave this as an exercise to the reader.

## Evolutionary Optimization with Go by Peter Bourgon
This talk was about the development of the project [oklog](https://github.com/oklog/oklog). Here Peter explains a great
development process. He made note to mention that there should be more "prototype driven design", which is the process
he describes this project took. To summarize: design, develop first, set a performance goal, optimize for the goal with
tools like pprof, stop once goal is met. There is no need to optimize code past that point it is needed.

## Functional Programming in Go by Aaron Schlesinger
This was an interesting talk. Aaron presented some functional programming paradigms and how to apply them in Go. He had
a [github repo](https://github.com/go-functional/core) that has some of this code pre-built out. I thought the talk was
interesting but to me functional programming, as cool as I think it is, does not seem practical in Go 1. Now if that Go
2 comes along with generics I think that this is a whole different story.

## grpc: From Tutorial to Production by Alan Shreve
This one was sort of just a tutorial, but that is okay because that is what I wanted from this talk. I think I will do
a blog post similar to this presentation in the future as I think more people need to start considering grpc. This
presentation is best described by just reading through the slides yourself I think. I will try to update with post in
the future when the slides have been made available.

## The New Era of Go Package Management by Sam Boyer
Here Sam talked about [dep](https://github.com/golang/dep), the future of Go dependency management. All I need to say
here is if you are a Go programmer get out and start using the tool now, it is ready for some prime time!

Until next time...

Cody out. `$ exit`