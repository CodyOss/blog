---
title: "GopherCon Day 0: Advanced Ultimate Go & Denver Go Meetup"
date: 2017-07-12T09:19:41-05:00
author: "Cody Oss"
categories: ["conferences"]
tags: ["go", "workshop"]
---
This year I had the great opportunity to attend GopherCon. A special thanks to to the company I work for, SPSCommerce,
for paying for my trip and conference, thank you. Before the conference began there were optional hands-on workshops
people could attend. I chose to enroll in the 'Advanced Ultimate Go with Bill Kennedy' course. I learned quite a bit
from this course and it was a lot of fun. Instead of doing an in-depth post on what I learned today though I am just
going to provide my raw unedited notes I took, as well as the public material we used.

After a day of learning I decided to Go learn some more at the Denver Go meetup. There I learned about 
[Go Kit](https://github.com/go-kit/kit) and [Gizmo](https://github.com/NYTimes/gizmo), two microservice frameworks
written in Go. It was more of a high level overview than anything else but it was cool since the people giving the talks
were the actual open source authors. I intend to try these frameworks out in my free time as I think they could be
valuable to use, especially in a 'enterprise' setting.

That is about all I have to say for today. While I am at Gophercon I will be most likely be publishing more "raw"
content like this as I want to focus on the conference. More detailed/overview posts will likely come in the following
weeks. Cody out. `$ exit`

## My Raw Notes
### Links
- [Material the workshop covered](https://github.com/ardanlabs/gotraining/tree/master/topics/go)
- [How to set-up Go](https://www.goinggo.net/2016/05/installing-go-and-your-workspace.html)

### Intro
- "we are the only industry that teaches people to write before we read. This is crazy" -- look up quote object c guy
- "history, language mechanics, design"
- when you set to early of a deadline you are writing legacy software. Know you will have to come back and clean up later
- "performance is not a priority, it is important". If it was use C not Go.
- "debuggers don't allow you to develop a mental model of your code". Don't use a debugger when code, only when trying to solve had problems.
- "if you do not understand the data you are working with you do not understand the problem you are trying to solve"
- 15 - 50 bugs per 1000 lines of code on average. So write less code.
- "error are not an exception, they are a part of the main code"
- "you are writing code for today, but designing for tomorrow"
- "you can not guess about performance"
- Sprint is twice as slow as Sprintf.... mind blown

### Pointers
- goroutine stack starts off at 2k
- go is pass by value natively wysiwyg(what you see is what you get)
- want to try to keep things off teh heap and only be on stack if possible. No heap means no GC
- construct values and return pointers if needed. Better readability
- `go build -gcfkags "-m -m"` will show you escape analysis
- escape analysis tries to determine if the value can stay on the stack and not the heap
- stack frame size is determined at compile time. `make([]byte,5)` is on the stack while `make([]byte, someVarSize)` will be on the heap
- anything shared between goroutines has to be on the heap
- If you are doing calculations in a loop use function calls. Or else there is no way for things like the GC to help clean things up.

### Arrays
- linked lists suck, array rock for mechanical sympathy
- our model is the "hardware"
- "when we lose focus on the data, we lose what we are doing"
- a slice of pointers is a linked list, not an array
- `for i, v := range something`: `something[i]` is a pointer to the original value, `v` is a copy value
- strings, ints, bools should always be pass by value
- everything is on the heap in java (sad panda)

### Decoupling
- code first in the concrete. Abstract and use interface later
	- prototype driven dev, not ttd (I like this)
- decoupling is about behavior
- never mix receiver types, exception is unmarshalling/decoding(always takes pointer)
- No constructors in, factory functions
- It is always safer to use pointer receiver
	- we want to use value semantics when we can to take pressure off the heap
- If a value function is a assigned to a var it is a snapshot of of the value at that time
- `read(int) ([]byte, error)` might seem like a good api for reader, but it would trash the heap in the process.
- interfaces do have the cost of an allocation
- for reference types use value semantics
- take pointers to structs, don't return pointers to structs!!!
- use functions first, not methods. Methods are the exceptions. Why create another type.

### Composition
- Don't group by who we are(type) group by what we do(interface)
- Don't embed type for state, do it for behavior

### Profiling
- `GODEBUG=gctrace=1` write GC work to stderr. This is how to get the pace of the GC
- `GODEBUG=schedtrace=1000` scheduler trace every so many milli
- import `_ net/http/pprof` to get free info
- `go tool pprof -alloc_space ./my-binary http://localhost:5000/debug/pprof/heap` heap profile
- hey is a load test tool
- `go tool pprof ./my-binary http://localhost:5000/debug/pprof/profile\?seconds\=5` cpu profile



