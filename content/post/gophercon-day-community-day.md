---
title: "GopherCon Day Community Day"
date: 2017-07-16T20:12:44-05:00
author: "Cody Oss"
categories: ["conferences"]
tags: ["go", "gophercon", "talks", "contributing"]
---

For community day I attended a couple different events throughout the day. I started off the morning with lighting
talks. There were quite a few and I took [loose notes which you can find below](#my-raw-notes-from-lightening-talks).
The talk that caught my attention most was the one on the new `sync.Map` package that can be found in the upcoming Go
1.9 release. I think I will do a blog on this package myself in the not too distant future.

After lunch I decided to attend the Go Contributors workshop. This class was awesome! I got to learn how to make
contributions to the Go programming language. The resources we followed for this class can he found
[HERE](https://docs.google.com/presentation/d/1ap2fycBSgoo-jCswhK9lqgCIFroE1pYpsXC1ffYBCq4/edit#slide=id.p).

*NOTE:* I am not sure if that deck will be there forever so if you are interested take a look sooner rather than later.

During the class we learned how to: sign the google CLA, set-up some git commands to work with gerrit (like GitHub, but
supposedly better for code reviews. I don't really think this is the case anymore, but I digress.), and make a change
to a scratch repo in the `x` packages of golang. Through this process we all learned the process each change set goes
through to make it into the upstream golang/go repo. 

After the class I felt inspired and I decided to try to find some easy issue I might be able to close. And I
[found one](https://github.com/golang/go/issues/20450)! And guess what?!?! My CL got accepted and I am now a
contributor to the Go programming language! You can see my
[commit here](https://github.com/golang/go/commit/91afca94e07aa1366afba9ece04c2def9f99d4c4)! I think in the future I
would also like to do a blog on how to contribute to Go. It was not nearly as hard or as scary as I once thought.

Well that about all I have for today. So until next time... 

Cody out. `$ exit`


## My Raw Notes from lightening talks
### Distributed Remote Monitoring /w 9volt
- title says it all 

### Interface Driven HTTP Responses
- not practical in my mind, but kinda cool

### Introduction to Hyperledger Fabric
- Distributed ledger / blockchain
- uses the endorsement policy (need 75% consensus)

### AI and Go 2 -- Landon
- TensorFlow go lib out
- check out pachaderm it is like git for data

### Polyglot REST Api and Code generation
- Open Api(The new swagger)
- 1.5 Mb JSON .5 sec to 9 milli when using Protocol buffer backed transport
- gnostic is the github project for this

### Powered game ai using TensorFlow in go -- neuro blaster dude (Pete something)
- Train your model in python first --> export trained model --> Deploy in Go ML 
- Data modeling is important
- github.com/faiface/pixel is a game lib in go
- Keras is a high level tool to build models in python, go still needs one...

### Becoming a better hacker -- lessons I learned from Poetry
- related writing code to poetry
- read, revise, persevere 
- stay hungry, stay foolish

### An overview of sync.Map Bran Mills
- pros
	- stable keys
	- disjoint stores
	- write once read many
	- concurrent loops
- replaces map + sync.RWMutex
- cons
	- reduced type saftey 
	- limited api
	- overhead
- a map of atomic pointers

### regex, do you need it?
- never inline compiling regex
- consider using string contains or prefix and suffix if you can, benchmarks appear to actually be faster
- benchmark all of the things

### Translating Go to other human languages and back again
- koro project replaces the keywords with symbols from other languages. Pretty dam cool!

### An Introduction to dep
- toml file is the one that you can actually edit
- will use ranges by default, use = if you really wanna lock it
- dep own the vendor dir, don't touch it after dep has control!
- dep ensure needs to be used if you don't check in vendor
- `dep ensure -u -n` is for a dry run of updating deps

### Anomaly detection in Go
- told a story 
- need to look more in how to do this

### Godzilla (ES2015 to Go transpiler and runtime)
- no vm or javascript interpreter
- pretty neat