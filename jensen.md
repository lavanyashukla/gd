Transcript
Note: Please submit any transcription corrections to angelica@wandb.com. Thank you!

Intro
Jensen:
For the very first time in human history, we are producing, manufacturing intelligence, like production. Raw material comes in. A lot of genius goes into that box. And what comes out is intelligence that's refined. 
Lukas:
You're listening to Gradient Dissent, a show about machine learning in the real world, and I'm your host Lukas Biewald.

Today on Gradient Dissent, I interviewed a guest that I've been looking forward to interviewing for quite a long time. This is Jensen Huang, who is the CEO and founder of NVIDIA. If you've trained a machine learning model, you've probably trained it on NVIDIA hardware. We get into machine learning and we talk about his views on what the future holds.

This is a super fun interview, and I really hope you enjoy it.

Why NVIDIA moved into the deep learning space
Lukas:
All right. Well, thanks so much for doing this. We collected questions from our community; they had a ton, so there's more questions that I'm sure we can get through. So I'm going to get into my questions first. 
Jensen:
Okay.
Lukas:
I wanted to start with the number one question I wanted to ask you which I've always wondered about. Which is, I think almost everyone training machine learning models these days uses NVIDIA, and I was really curious about how conscious of a strategy that was. Like when you started to think about it and how you made that happen. 
Jensen:
It started when almost simultaneously, three different research teams reached out to us, asking us to help them accelerate their neural network models. Turned out the reason for that was because they were all trying to submit for ImageNet, the big competition. And so deep learning came into our consciousness kind of around that time. 
Lukas:
What year is this? 
Jensen:
This is...when was Alex's ImageNet?
Lukas:
It must have been like 2011, maybe. 
Jensen:
Yeah, I was going to say 2012 or 2013. But anyhow, it's something like that. Anyways, AlexNet, it was that year. It was kind of around our consciousness around that time. 

The thing that was really exciting was...we all know that computer vision was hard to do. And for Alex to have created a neural network, trained it on a whole bunch of data, and broken a record of computer vision experts — of which many of them were at NVIDIA trying to do the same using human engineered features — that giant breakthrough caught a lot of our attention. 

Computer vision, as you know, is one of the foundations of artificial intelligence and all of a sudden a giant leap happened. And when discontinuity happens on something that important, it really caught our attention.

I think the difference between what happened around the rest of the world versus us is we took a step back and we said, "What is the implication of this?" Not just for computer vision, but ultimately how software is done altogether.

Recognizing that for the very first time software is not going to be written — features weren't going to be engineered or created by humans, but somehow automatically extracted out of data, refined out of data to recognize patterns, relationships, and somehow learn the representation of some predictive model — that observation early on caused us to ask the question, "How does this affect the future of software?"

How does this affect the future of computer science? How does this affect the future of computing? How would you change the way a computer...if the way that you write software is different, then how does it change the way you would design computers? And if the software that's written is written by a computer versus a human, how does that affect the type of computers you would design? 

We had the good sense of thinking about it — from first principles — the implications for the entire field of computer science and the entire field of industry. Which ultimately led to asking the question, "What about the implications to all the different industries?"

I think that the good fortune was we were interested in computer vision. We saw the gigantic breakthrough from Alex and Geoff Hinton and the folks at Toronto, and we simultaneously were working on it with several other labs at the same time.

So I think it was partly good fortune, partly having the sense to realize the profound implications to computer science, and then asking ourselves what the implication is for everything. 
Lukas:
I think one of the things that you've done amazingly well is just stayed dominant in this space. You might've had a head start, but of course, lots of other people have noticed that this is a really valuable space. And I've been hearing since maybe 2014 companies saying, "Hey, you know, we're going to make the next deep learning training...GPU or TPU," or something like that. 

But you've actually really maintained this ubiquity in the market, and I wonder what you attribute that to. Is it more the architecture of the chip or is it more the software, like CUDA and cuDNN? Or is it something else that kind of keeps you ahead of the competition? 
Jensen:
Well, partly because the company was formed properly for this opportunity. We were always in the field of accelerated computing.

If you could go all the way back to computer graphics, all the way since the beginning of our company, this new way of doing application acceleration — domain-specific application acceleration of which computer graphics is one; scientific computing and physics simulations and others is another; image processing, for example, is another; you could argue that deep learning is yet another — these different domains of applications, the company was started with that mission in mind.

Now, in order to do accelerated computing — domain-specific accelerated computing — you really have to be a full-stack company. You have to understand what is the application, the nature of the application you're trying to accelerate. You have to redesign the algorithm, because the way that you would write an algorithm, development algorithm, for sequential processing is radically different than parallel processing. Algorithm engineers, our company has a richness of algorithm engineers.

You have to think about the system software and the systems differently because the workloads change the bottlenecks. And so you have to think about system software differently, you have to think about systems differently, you have architecture of the chips differently.

Our company is fortunate that we are a full-stack company that goes all the way to the research of algorithms. That's what it really takes to be an accelerated computing company. 

But I think the advantage that we have is that we've been a full-stack computing company for a very long time. We have taken that skillset from computer graphics to imaging, to scientific computing. And then when deep learning came along, it was a problem that our company was very adept at solving.

Balancing the compute needs of different audiences
Lukas:
That's a good segue into a question a lot of people had that I have also, which is, "Is there a lot of tension between the needs of gamers and crypto miners and scientists and people in deep learning?" And how do you trade those off into a single chip? Like how do you prioritize the different needs?

Or maybe there's no tension because everyone has to do the same type of workload. I'm curious how you think about that. 
Jensen:
Yeah, there's absolutely a tension. 

For example, scientific computing...because it has a large body of historical code, and they could be in FP64, whereas for consumer applications, FP32 is just fine. Whereas for, deep learning, it's quite a large amount of different types of format that could be used.

The nature of the processing could be a little different. Sometimes it's very dense computation. Sometimes it's a little bit more sparse computation. Ray-tracing, for example, is very sparse. Rasterization on the other hand is rather dense. Image processing is rather dense. 

You have different computation natures. You have different precision that you have to support. Each one of the industries have a very large number of applications that are in use that you want to support and be able to accelerate. And so each one of these industries are a little different.

We try to build...we build a GPU that is universal, in the sense that all of these applications can run on any of our GPUs. And that gives developers a very large install base to target. They know that when they develop on our architecture, it'll run it everywhere.

The only question is, in each one of the processors that they run, is it better for scientific computing or is it better for machine learning or is it better for imaging or computer graphics? 

We shape the size of those capabilities — those functionalities if you will — for the different applications, different markets that we serve. In the case of GeForce there, there is no FP64 richness, although it runs. It runs rather slowly. In the case of deep learning chips, it'll run computer graphics, but it will run less well than GeForce and so on, so forth. 

We adjust the size of the functionality to the market that we serve. In combination with the software stack that goes on top of it, we should be able to bring the best products for the use case. 

Otherwise, everything is universal and everything just kind of works. Computer graphics, scientific computing, training inference. We really believe that developers ought to have the largest possible install base and not worry about whether the software's going to run or not. It should all always run. 

The question is whether it runs to its fullest capability. 

Quantum computing, Huang's Law, and the singularity
Lukas:
I see. 

Well, another question along those lines is, do you think radical changes are coming? In particular, do you think quantum computing is something really relevant to you? Like something that will be a practical reality in the next...in our lifetimes or the next five to ten years? 
Jensen:
It will definitely be in our lifetime because, Lukas, you and I are still pretty young. So we'll definitely see it. However it's not likely to, in the next five years, to be generally useful.

On the other hand, the important thing is — and this is really the marvelous thing about machine learning and deep learning — in many of the applications, whether it's drug discovery or large combination planning and optimizations (pathfinding, traveling salesperson problems) — these type of problems people have historically thought would need quantum computing...because of machine learning, because of AI, we've made giant leaps.

It's not, you know, Moore's Law-type leaps. If you look at the body of work of your customers, and our customers, and the scientists that work in both of our companies, in the last 10 years, where Moore's Law — if it was moving at full rate — would have increased performance by probably 100x, many applications — because of machine learning or deep learning — it's improved by 1,000,000x.
Lukas:
Totally. 
Jensen:
We've improved performance by a million times. And over the next 10 years, I fully expect that — because of a couple of different innovations between accelerated computing and the further advances that we're expecting in deep learning, and this new field called physics-informed neural networks, we're doing some really fantastic work there — in many areas in science scientific discovery, we're going to see probably another 1,000,000x. 

1,000,000x advance is something that's kind of hard to wrap your head around. But we're going to see that in so many different fields, whether it's in healthcare or climate science or other fields of physics that are really important to us.
Lukas:
Are you someone that believes that we'll see AGI in our lifetime? Do you think the singularity is coming? 
Jensen:
I don't know about that.

However, if we reframe the problem, if we reframe the question just slightly and say, "Will AI be able to do things that are much better than humans can?" You and I both know that, in fact, if you reframe the question that way, AI in many, many fields are already superhuman. And I think that the number of superhuman skills that AI will learn over the course of the next decade...it is quite extraordinary. 

I doubt that there will be many manipulation tasks that are repetitive, that robotics won't do better than humans. Which is one of the reasons why there's so much work in surgical robotics. Their hands will never shake. They'll be able to make the most minute and the most precise of incisions, and its perception ability is going to be incredible.

So I think that in the coming years, we're gonna see superhuman AIs. They won't be like us, but in many domains of activities, they'd be quite incredible. 
Lukas:
But I imagine where you sit, you're watching AI help with chip manufacturing and design better chips. And you're probably seeing that have compounding returns, which I think is sort of the thesis behind the singularity, right? It's sort of, AI starts to create AI. You just see this exponential... 
Jensen:
That's exactly right. 

Look, we're not going to be able to build next-generation chips without AI. And that's kind of a remarkable statement. 

That all of the chip design process, the architectural process...today we have 5 of the world's top 500 supercomputers in our company, and we are producing software that gets shipped with all of our AI chips. Without AI, we can't produce software that runs the AI. And in the future, without AI, we wouldn't be able to design the chips that we use to run AI. 

So that's right, the circular, positive feedback system is about to go into turbocharge. I have every confidence that the next 10 years, we're going to see even greater advances. Not necessarily at the transistor level, but absolutely at the computation level.

Democratizing scientific computing
Lukas:
Do you have any concerns about...as compute gets more and more important to advances in science, that there's impact on the climate or even impacts on access of who's able to make scientific discoveries or who's able to kind of make the next really exciting company if they need a supercomputer to do that?
Jensen:
First of all, one of our greatest contributions to the industry is we democratized scientific computing. Because of NVIDIA GPUs, the breakthroughs for AlexNet wasn't a supercomputer in the cloud, it was a GeForce card. 

Simultaneously, researchers around the world were buying GeForce GPUs. And because architecturally they're all the same as the supercomputers we're building, they were able to use that to discover the next...the breakthrough that we're all enjoying today. 

The same thing is happening in so many different fields. And so I'm really proud of the fact that we've democratized high-performance computing. We put it in the hands of any researcher. They don't have to go get gigantic funds to be able to do their research.

One of the scientists that was in quantum chemistry said to me one day that he had learned from his son, who was working at one of the computer companies here in Silicon Valley, that he should go and buy our gaming cards, and download the CUDA SDK, and port the quantum chemistry software that he was running on an IBM supercomputer onto our gaming GPU.

He was so amazed how fast it was. He had to wait for the rest of the week for the supercomputer to finish, so that he could compare the results, that it was the same. And then he went and bought as many GPUs as he could from the retail stores and made himself a bespoke...a homemade supercomputer.
Lukas:
That's awesome. 
Jensen:
He said to me, "You know, Jensen, because of your work, I'm able to do my life's work in my lifetime." In a lot of ways, we built him a time machine and he was able to see the future in a way that he otherwise couldn't. 

So I think the first contribution is we democratized scientific computing.

The second thing that we did...because of artificial intelligence and this idea of pre-trained models and transfer learning, we now have the ability to essentially have large companies pre-train intelligence. It's almost like creating a whole bunch of new college grads — super well-educated college grads — that are now going off into the world, that people can then adapt to their particular skills.

In a lot of ways, Lukas — the work that you do, the work that I do — what we've done is we've actually lowered the bar. We've democratized intelligence. We democratized computer science so that almost anybody can download a pre-trained model and perform superhuman capabilities for their application domain by retraining it, by adapting it, by applying a transfer of learning capability to it.

I think artificial intelligence is the most powerful force that has come along. And one of its benefits is going to be to democratize computer science. 

Now, one of the things that you mentioned earlier about energy...I think that one of the greatest projects we're working on is this thing called Earth-2, which is a digital tool which...we're going to try to build a digital twin to mimic the climate of the earth. It's a multi-physics problem, thermal dynamics and fluid dynamics and chemistry problem, and a biology problem, and the human driver problem, and economic problem.

All of it contributes in this geometry-aware...because, you know, terrain matters and multi-physics...and we finally might have the necessary algorithms to be able to take a swing at this and build a full-scale digital twin of the earth. And hopefully inspire us by giving us a model to test our mitigation strategies, and our adaptation strategies, and simulate whether the technologies we're going to use to absorb carbon or carbon emissions will have the necessary impact a decade, two decades, four decades from now.

If not for deep learning and the work that we're doing, that wouldn't even be possible. I wouldn't even imagine doing it.

How Jensen stays current with technology trends
Lukas:
Cool. 

One of the things I wanted to make sure I asked you, on a personal level, is I've really admired how you've run the same company for a really long time. It doesn't look like an easy company to run. 

I mean, there's a lot going on, and a lot of physical things, and it clearly hasn't just been this rocket-ship SaaS startup. And yet you seem very technically current. It really does seem like you stay on top of trends and keep a level of technical depth.

I was wondering how you do that, how you stay educated about what's going on in scientific computing and machine learning and other topics. 
Jensen:
Well, I'm a little sleepy right now because I was up at three o'clock reading and...there's just no other way. I think you just have to keep on learning.
Lukas:
You're just interested in the topic and you just-
Jensen:
-I don't know. I don't know that there's...I wish, Lukas, there was wisdom to pass. I paused for a second. Was there a secret? Nope. 

I think partly, of course, is really, "Where's the energy and the curiosity juice coming from?"

Being surrounded by really bright people, you learn from them, which allows you to combine a lot of your own understanding. And when you decode a puzzle or you learn something new, it really gets you fired up. 

I think one of the most important missions — and the purpose — of a CEO is to create the conditions where amazing people could do their life's work.

I really take that very seriously. I try very hard to create a condition where amazing people could come and be surrounded by other colleagues that are incredible. That, I think, contributes a lot to it.

And then the rest of it...as a CEO of a tech company, you really need to enjoy learning about what's happening in your company — which has plenty to learn — and what's happening around the industry, and see if you could imagine a future that's better for everybody.
Lukas:
I think a big part of my learning process that's hard to do running a company is tinkering and stuff. I'm wondering if that's...I think you're originally an engineer. Do you find time to ever write a little code or put something together? 
Jensen:
Not for a long time. But we get to tinker through other people.

This is the wonderful thing. NVIDIA is now 24,000 people. If I could tinker a little something with everybody, the amount of tinkering that's going around the company is incredible.

There's a phrase that I say. I reach out to my friends — and I really see them that way — I reach out to my friends all over the company, and we brainstorm a little something and they go off and try something and somebody else they're brainstorming with, they try something. That's, I guess, tinkering at scale. 
Lukas:
That's super cool. I love it.
Another question a lot of people ask...I'm curious, people originally think of NVIDIA as for games. Are you a gamer at all? Do you play video games?
Jensen:
I haven't played much games. 

I see almost every game that goes by, because we get the benefit of some collaboration that we do with just about every game company in the world. So when they're in the labs, people will tell me and I'll run down, and go check it out, and play with it a bit. 

But the last time probably...one of my favorite games was when Battlefield first came out. My kids were teenagers at home and they were both coming into their gaming age. And the three of us playing online Battlefield was just incredibly fun. That was probably some of the funnest memories I've ever had. 

The global chip shortage
Lukas:
That's awesome.

I'm curious. A lot of people have been talking about, you know, supply chain issues and a global chip shortage. Is that something that's on your mind a lot? Is that a problem for your company? 
Jensen:
Sure. Yeah, sure. 

We build the largest chips in the world and the most complex computers in the world. DGX is a few hundred pounds. It's so heavy. It's the heaviest computer that's being built today. It is so heavy that it takes a robot to build it, like a car. 

Most computers don't have to be built that way, but DGX is a miracle of computing. And we built it completely from a blank sheet of paper, wrote all the software and all the tools that went on top of it. There's a lot of components inside, especially...something that's a few thousand watts is quite a miracle.

There are a lot of parts, and all it takes is one diode or one voltage regulator to keep it from shipping. So our NVIDIA supply chain is quite an amazing machine. 

We know that artificial intelligence is such an amazing thing because we are producing intelligence. For the very first time in human history, we are producing, manufacturing intelligence, like production. Raw material comes in. A lot of genius goes into that box. And what comes out is intelligence that's refined. 

And so, large companies are depending on us. AI is intelligence being manufactured at large scales. So the teams are working really, really hard to keep up with demand. 

Leadership lessons that Jensen has learned
Lukas:
You've been running NVIDIA for quite a long time. I was curious how you feel you've changed as a leader over the decades of running the company.
Jensen:
You know, you're almost asking the wrong person. You could ask almost anybody else around me.
Lukas:
Fair enough. How has your experience changed? 
Jensen:
That's an easier question for me.
	
When I was 30 years old, I didn't know anything about being CEO. I did a lot of learning on the job. There were many management techniques that were just really dumb, and I don't use them anymore.
Lukas:
Like what? 
Jensen:
Well, alright. I'll give you a couple. 
Lukas:
Awesome. Thank you. 
Jensen:
The list of dumb things that I've done over the years is quite large. I could write a book. But for example, I really wanted, in the early days, for the chips to tape out. I thought what we needed to do was motivate the engineers to tape out the chip. So we had this thing called a "tapeout bonus". And that's just a supremely dumb idea. 

The reason for that is because if the engineers could have taped out the chip, they would have. Putting that bonus there is unnecessary. On the other hand, by definition, they're gonna be late. And when they're late, it becomes a de-motivator, because they no longer can earn a bonus. The tapeout bonus — for all the CEOs that are doing it — it's a de-motivator, not a motivator. It's a little silly. 

I think the answer is, a chip gets taped out when a chip is ready to be taped out.

We can create the conditions by which great work can be done. We can be good listeners and eliminate obstacles for the team. We could be part of the solution by highlighting issues, recruiting. All kinds of things that we can do to help them reason about priorities, help them reduce the scope of their work, and try to seek the minimum viable product instead of building such giant things. 

There are a lot of different skills that we could've instilled into the organization, but the one thing that it doesn't really need is a tapeout bonus, an achievement bonus. Because everybody's trying to do their best.

That's one example. 
Lukas:
That's a great one. What else? If you've got others, I'd love to hear them. 
Jensen:
Okay. Here's another one. Well, I want to be diplomatic as well, because there's so many CEOs that are out there. They could be using some of these techniques, and I hate to be critical of them. So this is not a criticism, this is just my style.

I tend not to do one-on-ones. If there's anything that I need to say, I tend to like to say it to the team and the group that is working on it, so that we're all hearing the same things. I'm hearing the same things, everybody else is hearing the same things, instead of being translated.
Lukas:
Interesting. That's a really unusual perspective. I think a lot of people think you absolutely must do one-on-ones. So you do that across the company? Do you think like your reports-
Jensen:
-I don't do it. I don't do it, but I have many leaders who do. I don't criticize them for doing it, I just don't do it. 

The reason that it's probably more important for CEOs not to, is because...you can't eliminate it completely, but you want to reduce the amount of, "Jensen told me," or "Jensen told me that," as a way to somehow steer a conversation that otherwise should have been done on merits. And instead of my will somehow being translated and repeated and interpreted through a chain. 

If I had a particular objection towards something, I would say it to more than one person. If I believe that in working with the rest of the company a particular strategy or direction ought to be taken, I would tell everybody at the same time. 

I've worked towards this approach because I feel it's much more transparent. It puts knowledge and the access to information in the hands of as many people as possible.

And of course it attracts more criticism to myself. For example, I might say something to ten people and it is the dumbest thing in the world to say. It was a terrible idea, you know, couldn't be a worse possible strategy. But instead of saying it to one person, I don't get the benefit of refining my ideas and then broadcasting it and always being a genius.

Therefore, in this technique, you need to be a little bit more vulnerable, and you need to be able to deal with the fact that every so often you said something that wasn't perfect. 

Nobody holds me to a standard that needs to be perfect, anyhow. And so I, after nearly 30 years, I've kind of worked my way past that. If I say something dumb, don't hold me to it. Give me a chance to change my mind.

Keeping a steady vision for NVIDIA
Lukas:
Is it a different experience, running a company where it feels like it's struggling versus now, where the stock seems really high and probably everyone's feeling really good about the prospects?

Do you have to do different things in those different situations? 
Jensen:
I'm never different. I don't think it's possible to find a correlation between my behavior and the stock price. And I would say for 29 years, my behavior and the way that I approach problems, the way I approach people, the way I approach a company or work...exactly the same. There's no correlation whatsoever. 

You just got to give me a second, I'll find all kinds of issues to talk about. I've got nothing but problems that...you know, CEOs are surrounded by problems, not good news

I happen to enjoy that. I enjoy solving problems. So I completely separate the financial success of the company from the importance of the work and doing impactful work. I've historically always done that, whether the company is doing well or badly.

When we were doing badly, particularly during the time when we bet the farm on accelerated computing — we wanted every single chip to have the same architecture that I mentioned earlier — the pressure on our financial performance was immense. But I was equally as enthusiastic then, and believed as much in the future, as I do today. 
Lukas:
That's incredible. You don't feel the outside pressure at all, or are you able to separate yourself from it? 
Jensen:
No, as a public company you're going to feel a lot of outside pressure. Some investors are really artful in expressing their displeasure and criticism, and some investors are understandably less patient. 

But it's our job to express the reason why we're doing what we're doing. CEOs have to be...we have to be reasoned. We have to have a purpose by which we're doing something. If we're clear in expressing why we're doing something, and our vision for it, and we genuinely believe it — we genuinely believe it — my experience has been that people are willing to give it a shot.

When we first started our company, consumer 3D graphics didn't exist. Even APIs for it didn't exist. We had to go evangelize that. And it took longer than people thought. When we moved into accelerated computing, for about 15 years it didn't exist. It took longer than I thought. I thought it was going to take 2 years, but it took 15.

AI was the same way. I spoke endlessly about the importance of machine learning and deep learning for the first 5, 6, 7 years. I think people just didn't get it. Which is fine. That's part of building a new market and building a new approach. You have to recognize that it takes time for people to come along.

I think the industry has been really patient with us, and our employees have been very patient with me. I've really appreciated it. 

Omniverse and the next era of AI
Lukas:
What's the thing that really motivates you right now? What's the purpose that you feel like you're serving at this moment?
Jensen:
Our mission...the company doesn't have a mission statement, but nobody's confused at our company in what the mission is. It really is as simple as, "Do impactful work," that takes a very long time to succeed — because it has to be hard for it to be meaningful for our people — and that we are the best in the world at solving.

We seek those problems. I seek those problems. 

There are two areas that I'm super excited about right now. 

One area is recognizing that we — in several domains — have invented the intelligence capability, the technology of intelligence. Whether it's in perception or speech AI or language understanding, we're now able to have some technologies that can do these things. 

However, ultimately what's valuable is not intelligence. Ultimately what's valuable is skills. We hire new college grads with lots of intelligence, but very few skills. And then we give them skills by adapting them to domains.

In a lot of ways, that's essentially...what is missing right now is to take the intelligence technology and translate it into valuable skills. Valuable skills, whether it's driving, autonomous vehicles. Valuable skills like customer service, and call centers, and such. Valuable skills like automated checkout. It could be automated skills like radiology. Put a radiologist right into the instrument.

There are all kinds of really valuable skills that we can now create. That's a big part of where our energy is right now, how to take this enabling technology and translate them into skills that customers in the industry, developers, could then adapt it for all kinds of different domains.

That's one, the large-scale application of artificial intelligence. 

Second, is the next era of AI. We've done a really good job with soft AI that's in the cloud. Recommending music, recommending movies and the next item in the cart, and so on and so forth. It's really incredible.

The thing that we would really like to do is to...if we want to take AI into the point of where people are and into this next phase of its journey, AI has to learn the laws of physics. 

Many of the world's challenges — whether it's climate science or autonomous vehicles or manufacturing or whatever it is — the AI can't just make a prediction. It has to make a prediction that obeys the laws of physics, conservation of matter, conservation of energy, and such.

It has to understand the concept of synchronous time. It has to be working within our time. There are a lot of these types of problems that are really impossible, to develop that AI unless we have something that is essentially a virtual world that obeys the laws of physics. Which is the reason why we built Omniverse. 

We built Omniverse so that several things could happen. It's physically based. It's distributed. It's very large. It has the ability to support very large models. And the goal is several fold.

One, you could teach a robot how to be a well-functioning robot in this physically based environment. You could connect it to IOT systems, for example, running a robot hardware in the loop. It has the ability to be connected to the physical world and stay synchronized, meaning to build a digital twin.

The concept of a digital twin has been around for some time, but in combination with artificial intelligence, the digital twin is going to have a profound impact on the future.

So, I'm super excited about these areas. One is just the application, and then the other's the next phase of AI. That's what Omniverse is all about. 
Lukas:
Yeah. I totally agree that things like Omniverse is really critical for making robotics work. 

It sounds like you're interested in getting your company closer to the applications of AI, is that right? 
Jensen:
We'll stay a couple of clicks away from the actual application. But what we would do is we would create an application framework for people who are building applications to build applications.

One of the application frameworks that I'm really excited about created a little demo. They called it toy Jensen, at the last (GTC) keynote. Basically, it's a robot. But it's a virtual robot, otherwise known as an avatar.
It has computer vision, it has speech AI and understands language. So on and so forth. I'm super excited about that because in the future, many applications...we really need to go into the application to experience it, whether it's a virtual factory or virtual hospital or what not. It could be for entertainment, like the metaverse and the next era of the internet.

You want to go into that world. And the way to go into that world is through a wormhole called VR. We can go into that world. But we could also have those agents come out of that world and collaborate with us. They would come out through the wormhole called AR, and be in our world. 

But otherwise, the metaverse is enjoyed using my favorite display, which is a computer display. People think that you need to wear head-mounted displays for the metaverse, but it's furthest from the truth. The metaverse will be enjoyed largely on 2D displays. 

ML topics that Jensen's excited about
Lukas:
Interesting. 

Well, we always end with two questions that I want to make sure that I get them in. The second-last question — and you've touched on some of these topics, but I'm curious — when you look at machine learning, do you feel like there's a question that's underexplored? Like you would recommend to a grad student to look into, or if you had more time you'd like to spend some more time investigating?
Jensen:
Well, some of the research work that's being done right now — there's so many smart people working on it because it's really important — the self-supervised learning approaches that are multi-modality...Lukas, that's going to drive the living daylights out of the platform you're building and the platforms we're building.

Multimodality AI, where you have vision — and the vision doesn't have to just be images. It could be video, speech, and natural language — that's going to take perception to a brand new level. I'm super excited about that. 

I'm excited about zero-shot learning. To be able to learn from whatever you're trained on, plus the priors that you have, is really quite exciting and powerful. 

I think that one of the areas that is being explored now is to project the framework of graphs into the framework of deep learning. Or, graph neural networks.

Graph neural networks...graphs, the relationship of things, is basically a structure that can describe almost everything meaningful in life. That's why it's so useful. 
Lukas:
Totally. 
Jensen:
But the processing of graphs is cumbersome. The breakthroughs with DGL, and GNN, and geometric, and all of that to project the graph into the framework, the constructs of a deep learning pipeline, puts it into our world where deep learning has been so effective. I'm excited about that, and I hope that a lot more people do that work.

Lastly, I think there will be more innovation and more design and more creativity that's going to be done in the virtual world, than all of the creativity and design that has ever been done in the physical world. 

What people call the metaverse is going to be just brand new ground for manufacturing, for design, for artists, for entertainment of all kinds. I'm super excited about that. I mean, there's so many things to work on. 

Why MLOps is vital
Lukas:
Awesome. That was a great answer. 

Our final question, in the last few minutes we have...there's this trope that machine learning, especially deep learning, projects almost never see the light of day. That they're way harder to manage than traditional engineering.

I'm curious. When you look across your customer base, what are the most common issues that prevent machine learning from really solving the problems that customers actually have?
Jensen:
Yeah, this is really great. It's a great question, and it's also one of the things I love the most about your company and the way you think about this.

There's a fundamental difference between the technology of deep learning and the harnessing of deep learning and machine learning to write software. The importance of the methods and the process and the tools, that is so vital. What could be described as MLOps, so vital. 

You have to understand not just the neural network architecture — and to be able to invent something that produces excellent results is of course groundbreaking work there already by itself — but a company, in order to take advantage of this, has to realize that in the final analysis, this is an intelligence factory.

You have to think of it like a factory. That's the reason why the word "ops" makes sense. It's a factory. 

You have the raw material coming in, which is the data. It gets transformed in the middle, through a lot of stages of very complicated transformation. Which is one of the reasons why your tools are so popular.

It's really complicated stuff. To manage that workflow in a productive way and transform that raw material into ultimately an output that is a neural network or otherwise intelligence-at-scale is quite a significant process. 

It's a fundamentally new way of thinking about computer science. We used to have just engineers do it. I don't mean "just" in that way, but we had engineers do it. But now we have engineers backed up by giant supercomputers that are operating these incredible operations — software stack — that you build. 

The refining process, the continuous refining process, the validation process, the simulation process...that entire process had to be reinvented for machine learning, reinvented for deep learning.

This is the reason why your work is so important. You guys are doing a great job. I really appreciate the work that you do, and all the researchers that you support, and all the workflows that you are making possible. 

This is what every company needs to understand. That software development in the future is a bit of a refinery process. It's a refinement process. It's an MLOps process. It's, you know, manufacturing. 

Outro
Lukas:
Well, thanks so much. That's really kind of you and I'm touched. I appreciate it. 
Jensen:
Keep up the great work.
Lukas:
If you're enjoying these interviews and you want to learn more, please click on the link to the show notes in the description where you can find links to all the papers that are mentioned, supplemental material and a transcription that we work were really hard to produce. So check it out.
