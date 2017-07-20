---
title: "GopherCon Day 1"
date: 2017-07-19T23:25:03-06:00
author: "Cody Oss"
categories: ["conferences"]
tags: ["go", "gophercon"]
---

So it is a little odd that I am posting this after my Day 2 summary, but that is life. At least I posted it right?

GopherCon 2017 Day 1 one jam-packed with lots of awesome things. Here are the highlights of each of the sessions I
attended.

**NOTE**: You can view the official live blog of the con [here](https://about.sourcegraph.com/go/) for more detailed info.
Slide decks can he found [here](https://github.com/gophercon/2017-talks)

## Go Reliability and Durability at Dropbox by Tammy Butow
This talk outlined how and why Dropbox uses Go. Tammy shared some cool information on how they onboard new engineers at
Dropbox. I liked how it was through building a project. I think more places need to do this type of onboarding. She also
touched on some things like how they upgrade to new versions of Go. It was cool for me to hear how big companies,
besides Google, use and manage Go at the workplace.

## The Future of Go by Russ Cox
So this was kinda a big one. Russ started off all nice and slow in talking about the history of Go. Then he transitioned
to what everyone wanted to hear about: Generics. JK.(Well kinda) He actually brought up how now is the time the Go team
wants to start gathering and sourcing ideas for Go 2. The words "generics" were brought up but not in the way a lot of
people would hope. Basically he said what people need to do is outline use-cases for adding new features like generics.
To make things clear he outlined a process how how to evaluate new features added to the language. It was also stressed
that once Go 2 is a thing they want to make the transition as seamless as possible to get mass adoption quickly. I am
looking at you Python 3.

## Generating Better Machine Code with SSA by Keith Randall
I am not going to lie, this talk was a bit over my head. That is not to say Keith did not do a good job presenting, he
did. It was just on a dense set of material. It was interesting to hear about the compiler though. I think one of these
days I might just have to take a deeper dive and try to understand this better. But until I do I would just recommend
looking at the official blog for a more detailed summary.

## A Go Programmer's Guide to Syscalls by Liz Rice
Speaking of things that were over my head. Just kidding this one was not so bad. I think if a different person other
than Liz gave this talk, it could be a disaster and boring. But she somehow made learning about syscalls not boring. 
During her talk she implemented, and explained well, how to write Strace in Go in ~60 LOC. Pretty cool.

## Valuable Lessons in Over-Engineering the Core of Kubernetes kops by Kris Nova
Here is what I learned from this talk in a nutshell, don't mix a lot of YAML and `text/template`. While working on kops
Kris and others were noticing it was becoming hard to support and there code was panicing more than they would like. 
This is because they were making heavy use of templating and YAML files, effectively creating there own programming
language that was hard to maintain and impossible to test. The solution? Rewrite 1000 lines of YAML into 10 Go structs.
Now there is type safety and the code is much easier to test. Favorite slide from the deck, 'Things we need to fix? 1. 
Our Shit'. :)

## Go Anti-Patterns by Edward Muller
This one was really about how to write idiomatic code by not writing shitty code. Edward listed off some good anti-patterns
to avoid when possible. To summarize:

- Tiny Package Syndrome: one file packages that do little
- Premature Exportation: no need to export if not needed
- package `util`: name it something better, packages are for grouped behavior
- config structs: try things like functional options when possible
- pointer all the things: guess what, pointers almost always go on the heap, sometimes it is cheaper to make a copy
- context.Value: avoid. (not sure how much I agree with this, but you have to exaggerate a little when presenting...maybe?)
- async APIs: avoid returning channels(yes, but I think some cool projects can be made using this pattern)
- if-else: things a good linter fix for you
- Panic in a lib: don't because that is just mean
- Interface all the things: interfaces have a cost and are not always needed.(Go != Java)
- interface{}: try to tease out real interfaces when you can

## Forward Compatible Go by Joe Tsai
This talk was a little different. Joe focused on saying don't couple too tightly to anything or it might break on 
upgrade. There were some solid examples talking to the `time.Time` package in particular. The key take away here is you
should read the docs and see what they say is happening. Don't rely on side-effects that might not always be there. Go 1
guarantees APIs, not the code that backs them necessarily.

Cody out. `$ exit`