Jeremy Howard — The Simple but Profound Insight Behind Diffusion
Jeremy explains diffusion, shares his thoughts on large models, revisits the debate between Python and Julia, and talks about his scientific advocacy during the early days of COVID-19.

Timestamps
0:00 Intro
1:06 Diffusion and generative models
14:40 Engaging with large models meaningfully
20:30 Jeremy's thoughts on Stable Diffusion and OpenAI
26:38 Prompt engineering and large language models
32:00 Revisiting Julia vs. Python
40:22 Jeremy's science advocacy during early COVID days
1:01:03 Researching how to improve children's education
1:07:43 The importance of executive buy-in
1:11:34 Outro
1:12:02 Bonus: Weights & Biases

Transcript

Intro
Jeremy:
I’ve been telling everybody who will listen that I feel like we’re in the middle of a significant spike in technological capability right now. And so if you’re not doing that, you’re missing out on being at the forefront of something that’s substantially changing what humans are able to do.

Lukas:
You're listening to Gradient Dissent, a show about machine learning in the real world. I'm your host, Lukas Biewald.
Jeremy Howard is the founding researcher at fast.ai, which is a research institute dedicated to making deep learning more accessible. They make an incredible Python repository that people use for lots and lots of deep learning projects. And they make an incredible set of classes that many people I know have taken, and is almost universally loved. He was also the CEO and founder of Enlitic, the president of Kaggle, and has done a whole bunch of diverse, amazing things in his career.
It's always super inspiring to talk to Jeremy and this interview is no different. I really hope you enjoy it.


Diffusion and generative models
Lukas:
You are the first person to be on this podcast two times. And I think you are the most popular guest that we've had, based on our YouTube metrics. So it's great to have you.
I wanted to start with, actually...the most memorable part of our interview — for me personally — was the amount of time that you set aside every day to work on just learning. Undirected, sort of learning new things, which I really thought was an amazing thing that I always aspire to do more of.
I was curious. Lately, what have you been learning?

Jeremy:
I'm spending all my spare time at the moment on generative modeling, around the Stable Diffusion or diffusion modeling space.

Lukas:
Hence the new course, I guess. Is that part of the learning process?

Jeremy:
Yeah. It’s a chicken and the egg thing. It's partly "the new course is because of the learning", and partly "the learning is because of the new course".
I've been telling everybody who will listen that I like feel we're in the middle of a significant spike in technological capability right now. And so if you're not doing that, you're missing out on being at the forefront of something that's substantially changing what humans are able to do.
When there's such a technological shift, it creates all kinds of opportunities for startups, and for scientific progress, and also opportunities to screw up society. Which hopefully you can figure out how to avoid, and stuff like that.
I'm very keen to do what I can to be on the forefront of that, and to help others who are interested in doing the same thing.

Lukas:
When you say "spike", do you mean diffusion models specifically or do you mean machine learning more broadly? Do you mean like-

Jeremy:
-I mean diffusion models, specifically.

Lukas:
Interesting, interesting.

Jeremy:
Yeah. It's a simple but profound insight. Which is that it's very difficult for a model to generate something creative, and aesthetic, and correct from nothing...or from nothing but a prompt to a question, or whatever.
The profound insight is to say, "Well, given that that's hard, why don't we not ask a model to do that directly? Why don't we train a model to do something a little bit better than nothing? And then make a model that — if we run it multiple times — takes a thing that's a little bit better than nothing, and makes that a little bit better still, and a little bit better still."
If you run the model multiple times, as long as it's capable of improving the previous output each time, then it's just a case of running it lots of times. And that's the insight behind diffusion models.
As you'd be well aware, Lukas, it's not a new insight. It's the same basic insight that belongs to this class of models called "boosted models".
Boosted models are when you train a model to fix a previous model, to find its errors and reduce them. We use lots of boosted models. Gradient boosting machines in particular are particularly popular, but any model can be turned into a boosted model by training it to fix the previous model's errors.
But yeah, we haven't really done that in generative models before. And we now have a whole infrastructure for how to do it well. The interesting thing is that — having started to get deep into the area — I've realized we're not close at all to doing that in an optimal way.
The fantastic results you're seeing at the moment are based on what, in a year's time, will be considered extremely primitive approaches.

Lukas:
Could you say a little more about that?

Jeremy:
Sure. Broadly speaking, we're looking to create a function that, if we apply it to an input, it returns a better version of that input.
For example, if we try to create a picture that represents "a cute photo of a teddy bear", then we want a function that takes anything that's not yet "a really great, cute photo of a teddy bear" and makes it something a little bit more like "a cute photo of a teddy bear" than what it started with. And furthermore, that can take the output of a previous version of running this model and run it again to create something that's even more like "a cute version of a teddy bear".
It's a little harder than it first sounds, because of this problem of out-of-distribution inputs. The thing is if the result of running the model once is something that does look a little bit more like a teddy bear, that output needs to be valid as input to running the model again. If it's not something the model's been trained to recognize, it's not going to do a good job.
The tricky way that current approaches generally do that, is that they basically do the same thing that we taught in our 2018-2019 course, which is what we call "crap-ification". Which is, to take a perfectly good image and make it crappy.
In the course, what we did was we added JPEG noise to it, and reduced its resolution, and scrolled[?] text over the top of it. The approach that's used today is actually much more rigorous, but in some ways less flexible. It's to sprinkle Gaussian noise all over it. Basically, add or subtract random numbers from every pixel.
The key thing is then that one step of inference — making it slightly more like a cute teddy bear — is basically to "Do your best to create a cute teddy bear, and then sprinkle a whole bunch of noise back onto the pixels, but a bit less noise than you had before."
That's, by definition, at least going to be pretty close to being in distribution, in the sense that you train a model that learns to take pictures which have varying amounts of noise sprinkled over them and to remove that noise.
So you could just add a bit less noise, and then you run the model again, and add a bit of noise back — but a bit less noise — and then run the model again, and add a bit noise back — but a bit less noise — and so forth.
It's really neat. But it's like...a lot of it's done this way because of theoretical convenience, I guess. It's worked really well because we can use that theoretical convenience to figure out what good hyperparameters are, and get a lot of the details working pretty well.
But there's totally different ways you can do things. And you can see even in the last week there's been two very significant papers that have dramatically improved the state of the art. Both of which don't run the same model each time during this boosting phase, during this diffusion phase.
They have different models for different amounts of noise, or there are some which will have super resolution stages. You're basically creating something small than making it bigger, and you have different models for those.
Basically, what we're starting to see is that gradual move away from the stuff that's theoretically convenient to stuff that is more flexible, has more fiddly hyperparameters to tune. But then people are spending more time tuning those hyperparameters, creating a more complex mixture of experts or ensembles.
I think there's going to be a lot more of that happening. And also, the biggest piece I think will be this whole question of, "Well, how do we use them with humans in the loop most effectively?" Because the purpose of these is to create stuff, and currently it's almost an accident that we can ask for a photo of a particular kind of thing, like a cute teddy bear.
The models are trained with what's called "conditioning", where they're conditioned on these captions. But the captions are known to be wrong, because they come from the alt tags in HTML web pages, and those alt tags are very rarely accurate descriptions of pictures.
So the whole thing...and then the way the conditioning is done has really got nothing to do with actually trying to create something that will respond to prompts. The prompts themselves are a bit of an accident, and the conditioning is kind of a bit of an accident. The fact that we can use prompts at all, it's a bit of an accident.
As a result, it's a huge art right now to figure out like, "trending on art station, 8k ultra realistic, portrait of Lukas Biewald looking thoughtful," or whatever. There's whole books of, "Here's lots of prompts we tried, and here's what the outputs look like".
How do you customize that? Because, actually, you're trying to create a story book about Lukas Biewald's progress in creating a new startup, and you want to fit into this particular box here, and you want a picture of a robot in the background there. How do you get the same style, the same character content, the particular composition? It's all about this interaction between human and machine.
There's so many things which we're just starting to understand how to do. And so, in the coming years I think it will turn into a powerful tool for computer-assisted human creativity, rather than what it is now, which is more of a, "Hand something off to the machine and hope that it's useful."

Lukas:
Do you think the same approach applies across domains? Or is there something about images — the way it's sort of obvious how to add noise — and maybe the data set that we have?
I mean, certainly the way you described diffusion, there's a natural application to that to almost any domain, but-

Jeremy:
Correct.

Lukas:
-I guess Gaussian noise on text, it's a little unclear to me what that really means. Maybe it’s like...

Jeremy:
So, last week a paper showing diffusion for text came out.
There's already diffusion models for proteins. There's already diffusion models for audio. The audio ones use — or some of them — use a fairly hacky obvious but neat approach of using diffusion to generate spectrograms — which are images — and then having something like a super resolution model. But it's not doing super resolution, it's doing spectrogram to sound.
So yeah, these things are already starting to exist. They haven't had as much resources put into them yet, so they're still not that great. But yeah, that's the thing, Lukas, this is not just images at all. It'll be used in medicine, it'll be used in copywriting. The way we currently do generative text models, again, it's kind of a happy accident.
When I did ULMFiT, the whole reason I created a language model was for the purpose of fine-tuning it to create a classifier. GPT then took that idea and scaled it up with Transformers. What Alec Radford was trying to do there was not "generate text", but try to solve other problems by fine-tuning it.
There was this kind of discovery, almost, with GPT-3 that when you take this and you scale it far enough, it actually starts generating reasonable-sounding text. But the text is not necessarily correct. In fact, it's very often wildly incorrect. It'll...intentionally working on text generation approaches which are specifically designed for generating text is something that there's a lot of room to improve. 
Generally speaking, the way I see it is this. You've got a generative model that's trying to do something difficult and it's pretty good at it, or at least better than nothing. It'll be better at it if you can do it in a way that it runs multiple times during inference, because you're giving it more opportunities to do its thing.
I think that means that these multi-step inference models — which may or may not be diffusion models, but kind of boosted generative models — are here to stay. Because no matter how good your generative model is, you can always make it better if you can find a way to run it multiple times.


Engaging with large models meaningfully
Lukas:
I guess that is a good segue to another question I had, which is I think one of the really fun things about deep learning in the early days was it was so tangible. You have this fantastic class, where you can just kind of build these models and see how they work and play with them. I think we both have a very similar learning approach.
But, one thing I've personally been struggling with, honestly, with these bigger models is just actually engaging with them in a meaningful way. It's fun to run the various image-generating models, but it feels kind of daunting. I'm not sure I have the money myself to buy the compute to make one that really works. 
We actually had one person on this podcast who did it for fun — Boris — which is a super fun episode, and I felt really jealous of how much fun he had building it. I'm curious how you turn that problem into something tractable, that you can actually engage with.

Jeremy:
Yeah. Well, Boris is one of our alumni. He's part of our fastai community, and he showed what is possible for a single, tenacious person to do.

Lukas:
Although I think Google donated like a hundred thousand dollars of compute to him. So it wasn't totally...

Jeremy:
Yeah, absolutely. If you can show that you're doing useful work, then there's plenty of compute out there which you can get donated to. But having said that, what he was largely trying to do — at least at the outset — was to replicate what OpenAI had done.
I take a very different approach, which is I always assume that the best thing out there right now is far short of what the best thing could be. That in five to ten years time, there'll be something better, and I always look for improving that.
So yeah, you should take our new course, Lukas-

Lukas:
I would love to.

Jeremy:
-which we're in the middle of, because what I've been working on is exactly what you describe. Which is, how to train and play with a state-of-the-art image-generative model in a notebook on a single GPU. 
As with all of these things, the trick is to start with an easier but equivalent problem.
I'm doing all my work — just about — on the Fashion-MNIST dataset. Which, rather than being 512x512 pixel images of literally anything in the world, including artworks, in three channels, Fashion-MNIST is 28x28, single-channel images of 1 of 10 types of clothing.
I always tell people — whether you're doing a Kaggle competition, or a project at work, or whatever — the most important two steps are to "Create a rapid feedback loop where you can iterate and test fast", and to "Have a test which is highly correlated with the final thing you're going to be doing."
If you have those two things, you can quickly try lots of ideas, and see if they're probably going to work on the bigger dataset, or the harder problem, or whatever.
It turns out Fashion-MNIST basically...I've kind of replicated a bunch of different approaches in the literature on Fashion-MNIST. The relative effectiveness of those different approaches on Fashion-MNIST mirrors basically exactly their relative effectiveness on COCO, or ImageNet, or LAION, or whatever.

Lukas:
Cool.

Jeremy:
But I can train a model on a single GPU to a point where I can see relative differences in about two minutes.

Lukas:
Wow.

Jeremy:
And that means I can very rapidly try things. I've started building notebooks where I show every single little step. And also, it helps a lot to use notebooks, which almost nobody working in the generative modeling field seems to be doing at the moment. 
What they do, is they have...the normal approach is to do ImageNet 64-pixel or CIFAR 32-pixel —  which is still better than doing 512x512 LAION — but it still takes...ImageNet 64-pixel takes many hours on an 8-GPU machine. You can't do a fast iteration loop.
In a notebook, I can run a single iteration of diffusion. I can see what the outputs look like because the pictures are all there in front of me. If you're not using this kind of approach, instead you're switching back and forth between a terminal, and then you need some way of actually viewing the images. And given that you're probably not sitting directly on that 8-GPU box, you're probably SSH-ing into it. So, now you've got to find a way to show those pictures.
There are ways, by the way, of showing pictures in the terminal. For example, if you use iTerm2 there's something called imgcat. If you use other terminals, they probably support something called sixel, sixel graphics. But there's...they're not going to be as a good exploration environment for the kind of stuff than a notebook is.
I think there's lots of opportunities for people like you and me to play in this field. I mean, I know there is because I've started spending time talking to some of the folks who were the primary researchers responsible for the key components of Stable Diffusion. And I'm already telling them things that they hadn't thought of before, by virtue of weird little experiments I've done with Fashion-MNIST on my single-GPU Jupyter Notebook.


Jeremy's thoughts on Stable Diffusion and OpenAI
Lukas:
Yeah, that makes sense. A fast feedback loop is so important. That's very cool.
I was curious, broadly, if you have though on Stable Diffusion in general. We're sitting here in November 2022, and I think they've done an amazing job of bringing awareness to generative models.
What do you think about Stable Diffusion?

Jeremy:
It's been great for progress in the field, clearly.
Generally speaking, I'm all about democratization and accessibility, as you know. I don't love the fact that before Stable Diffusion was released, a small number of people in the world had access to the full generative models. And then other people could pay for cut-down versions of them, use them in small quantities. 
The thing is, accessing these things through a web-based API is extremely limiting. When you've actually got the weights, you can really play with both the engineering and the artistic side of doing things that no one's done before.
So yeah, I think that's great. I think it's important.
I think — as with any of these things — you release a new, powerful technology out there and a whole bunch of people are going to be using it for, you know, not necessarily the things that you would have chosen to use it for.
For example, for Stable Diffusion, it seems like a very large percentage of people who are using it to generate lots and lots of images are doing it to generate anime and specifically nearly entirely...very young women with very few clothes on, anime pictures. I'm sure there are people out there who are taking the clothes off entirely.
That happens, I guess, with any technology. I don't necessarily have...I mean, I guess you can't stop that happening. But we certainly need appropriate laws around at least making illegal things...make sure the things that we don't want to be legal, are in fact illegal.
But yeah, there are obviously huge benefits. And you're not going to get stuff like protein diffusion models, or pharmaceutical diffusion models...none of those are going to develop if the technologies are in the hands of two or three big organizations.
So it's certainly a very valuable step on the whole for society to have this stuff as open as possible. And to be clear, it was all trained at universities. The main one, most of the stuff we're using now for Stable Diffusion was trained in Germany, at German academic institutions, using donated hardware.

Lukas:
I guess it's interesting though that it was, I think, primarily ethics and AI considerations that made folks like OpenAI restrict access to their models. Or at least that's what they said.
Do you think that you would know a priori that that was the wrong thing to do? Would you have pushed against that at the time?

Jeremy:
I actually wrote a blog post about that back when GPT-3 was just announced, and not released. Nearly universally, the feedback — at least from the AI community — was, "Oh, this is lame. They're just doing it for profits." In my blog post, I said, "Well, not necessarily. There are genuine things to be thinking about here."
Which is not to say that that means that the motivation wasn't at least partially profit-driven. It might well have been. It's certainly convenient that the ethical considerations read in this way entirely align with profit-driven motives as well. But, like I say, it doesn't necessarily mean they're not true. And I'm pretty sure it's for both reasons.
If you look at the way OpenAI has behaved since then, they've behaved in a way that is very increasingly apparently profit-driven. So, I'm less generous in my interpretation now than I was then, based on their continuing patterns of behavior.
I think also with the benefit of hindsight, it feels a lot more like, in the last couple of years, companies keeping models to themselves, the main impact that ends up being is to create a bigger bifurcation between haves and have-nots in terms of capability. Requiring more researchers to pay for API access to do things, a decreased amount of openness, and in fact even what could be argued as being kind of deceitful behavior.
For example, we now know that the OpenAI models that you can pay to access are actually not the same as what's been described in their research papers.
We've now had dozens of people write research papers comparing various work to the OpenAI models, and now we've learned that actually we're not comparing to what we thought we were comparing at all. You know, thousands of hours of researcher time being wasted and papers being published with what turns out now to actually be totally wrong information.
I'm definitely more enthusiastic about the idea of being open than perhaps...more confident about that than I was a couple of years ago.


Prompt engineering and large language models
Lukas:
Do you have thoughts on the language side of things, like large language models?
Do you think that...for example, do you think that prompt engineering is headed to be an important way of doing machine learning? You do see these models doing incredibly well in a wide variety of NLP tasks. Better than models trained specifically on these specific tasks, sometimes.

Jeremy:
Yeah. I think generative text models have both more opportunities and more threats than generative image models, for sure.
Like I say, they're kind of...the fact that they work at all is in some ways a bit of an accident. They're far, far, far from being optimized for purpose at the moment.
But they're already amazingly good, particularly if you do this kind of stuff where literally there are now dozens of papers. "Just look at what kind of prompts happened to work on these models that we kind of accidentally made generative models," "let's think step-by-step", and whatever else.
We're starting to find ways to actually get them to do a little bit more of what we actually want them to do. But so far we're using really, really basic things. You know, all this "instruction tuning". 
So, rather than just feeding it the entire internet, let's actually fine-tune it with some examples of things that are actually correct info, that actually represent outputs that we would want for these inputs, rather than just whatever somebody rando wrote on the internet 25 years ago.
My worry is...I'm much more worried about misuse of text models and image models, because it wouldn't be at all hard to create a million Twitter or Facebook or whatever accounts, and program them to work together to impact the world's discourse in very substantial ways over time.
And nobody would know.
We could have...on Twitter, for example, some fairly small number of accounts — often where nobody actually knows the human who's behind it — can have very substantive effects on what people are talking about, and how people talk about that thing.
Imagine a million of those accounts, which were actually bots that had been trained to be more compelling than humans — which already for years, we've had bots which humans rank as more compelling than actual humans — and that they've been trained to work together. You know, "Take alternate points of view in exactly the right way," and this bot gradually gets convinced by that bot, and whatever else.
It could cause a very small number of people in the world to programmably decide how they want humanity to think about a topic, and pay to make that happen.

Lukas:
Although if I remember right, it seemed like all of fast.ai's sort of broad mandate was to basically make a no-code interface into machine learning, so anyone could access it. And it does sort of seem like prompt engineering — to the extent that it works — is like a huge step in that direction. Isn’t it?

Jeremy:
Right. Yeah, that's what I'm saying. That's why I said it's both got more opportunities and more threats.
The opportunities are vast. Take, for example, the recent thing that was released last week or so, explainpaper.com. Where our students are already...so, with our course we look at a paper or two each week. Last week I had told the class, as homework to re-implement the diff edit paper.
Students were saying like, "Oh, I didn't understand this paragraph. So I highlighted it in explainpaper.com, and here's a summary it gave, and that's a lot more clear now. And then I tried to understand that bit, so I asked for more information."
This is very, very valuable.
I saw somebody on Twitter a couple of days ago saying they don't really use Stack Overflow anymore, because they created this tiny little, simple little script called "ask" where they type "ask" and then something as a prompt — sorry, in the bash shell repl — and it would feed that off to OpenAI GPT-3, and return the result, and they basically use that instead of searching the internet nowadays.

Lukas:
Wow.

Jeremy:
Yeah. People are definitely using this stuff and it's going to get much, much better.

Lukas:
Do you have a clever way — like with Fashion-MNIST and image generation — to play with large language models on kind of a bite-sized scale?

Jeremy:
Not yet, no. I'll get to that, maybe, in another part of the course, I guess. It's definitely a great question and something to think about.


Revisiting Julia vs. Python
Lukas:
Interesting.
Okay, a question that I need to revisit — because this is unexpectedly, I think, one of the reasons that so many people listened to my interview with you last time — you sort of made an interesting comment that you felt like Python wasn't the future of ML.
You sort of said maybe Julia is the future of ML, and that really seemed to strike a chord with the internet everywhere. I think it's kind of the most-discussed part of Gradient Dissent of all time.
So, I'm just curious. Do you have any more thoughts on that? Do you still believe that Julia is the future? You were sort of on the fence about that.

Jeremy:
I was on the fence about that last time we spoke and-

Lukas:
Totally.

Jeremy:
-I would say I'm a little less bullish than I was then.
I feel like the Julia ecosystem and culture, it's so focused on these HPC, huge compute, running things on national lab machines. It's all stuff that's very appealing to engineers. It feels good, but it's such a tiny audience.
I don't care about whether I can run something on 5,000 nodes. I just want to run it on my laptop. And it's still not great for running on my laptop, really. And it's not great for creating software that I can send you.
I can't...if I created a little CLI tool or whatever, well, it's not great for creating little CLI tools cause it's so slow to start up. And then how the hell am I going to send it to you to try out? 
It'd be like, "Okay, Lukas. Well, install the entirety of Julia, and then run the REPL, and then type this to go into package management mode." And then, "Okay, now you've got this thing and now you can run it." It's like, okay, that's not going to happen.
Or even just deploying a website, it's a lot of fuss and bother, and uses more resources than it should.
It's still got that potential. But...I guess the other thing that's become more clear, though, in the last couple of years is their grand experiment on type dispatch...it is more challenging to get that all working properly than perhaps I had realized, because it's still not really quite well working properly.
Good on them for trying to make it work properly. It's a vast research project. But there's a lot of weird little edge cases and trying to make that all run smoothly is incredibly challenging.
I suspect...something needs to replace Python, but maybe it's something that doesn't exist yet. Partly though...what we're seeing instead...everybody knows we have to replace Python. So, what instead's been happening is we're using Python to create non-Python artifacts. Most obviously JAX.
JAX uses Python — or a subset of Python — with a kind of a embedded DSL written as a library. Which only lets you create things that can be expressible as XLA programs, and then XLA compiles that to run fast on a TPU That works pretty well.
It's very challenging, though, for research, or hacking, or learning, or whatever, because it's actually not Python that's running at all. So it's extremely difficult to profile — and debug, and so forth — that code. Very hard to run it really nicely in notebooks.
In our little team working on diffusion models, we kind of all want to use JAX. But every time we try, it's always...because like everything I write is always wrong the first 14 times.
And with Python, you know, I have 14 goes at making it better by finding all the stupid things I did. By running one line at a time, and checking things, and looking at pictures. With JAX, I wouldn't know how to fix my broken code, really. It's difficult.

Lukas:
But you don't think that that flexibility is fundamentally in conflict with making a language performant? I think we covered this last time.

Jeremy:
It is for Python. It is for Python, I think.
For Python, that flexibility is to be able to actually run it as Python code. If you look at where PyTorch is going now, they've got this TorchDynamo stuff where they're working...they basically can interface with nvFuser, and you can interface with Triton, the OpenAI compiler-ish thing. I'm not sure exactly sure what you'd call it.
Clearly PyTorch is heading the same direction as JAX. Which is, if you want it to run fast, you'll use TorchDynamo, or whatever it ends up being called. That's actually now integrated into the PyTorch tree. That's clearly where we're heading. And again, you end up with...probably you'll be using Triton.
So you end up...Triton's amazing. Super cool, super fantastic. But you still end up with this thing that's running compiled code. It's not the same code you wrote, but a version of it. More difficult to hack on.
If you look at how this works, there's a whole world of software that's written in languages which were explicitly designed to work this way. They're compiled languages. Languages like C++, and Swift, and Rust. They have something very nice, which is they have flags you can pass the compiler.
You can pass that the -d flag to run it in the debugger, or you can pass the -o flag to run the optimized version. Basically, you get to choose how close the code that's actually running is to the actual lines of code that you wrote.
So that for debugging, you can actually...it'll run slower, but it's actually running the lines of code that you wrote. And I think we want something like that, something that, "Yeah, it looks like Python. It's pretty compatible with Python. You can still run it as Python, but you can also run it in an optimized way." Maybe something that actually takes better advantage of these kind of type hints that we can provide.
That's my guess. What's going to happen is we'll see Python-esque languages...we'll continue to see these Python-esque languages appear, that may begin to look less and less like pure Python, and are designed to work better and better with these backend linear algebra accelerators and compilers.

Lukas:
Is there some language out there right now that that has that feel for you?

Jeremy:
No, they're all basically these embedded DSLs. Like TVM or like Halide.
We have the MLIR project, which is kind of providing the backend needed for these kinds of things. Chris Lattner has a new company, which presumably is going to be placed better than any other to create what we need for this kind of thing. He's the guy behind MLIR.
It feels like a big open area to me, at the moment.


Jeremy's science advocacy during early COVID days
Lukas:
Interesting.
Okay, on a totally different topic — that I kind of can't believe we didn't cover last time, I feel like we must have been right in the middle of it — I think I, along with many other people in the world, watched you advocate for wearing masks in the early days of COVID.
I think you had some of the most high-profile articles on this — like the second-most popular on Preprints — and I was just kind of curious if you could sort of tell that story from your perspective. And maybe what you were seeing that other people were missing, and how you were kind of approaching that problem differently.

Jeremy:
It's hard for me, Lukas, because I don't understand why — and I still don't understand why — it's not reasonably obvious to everybody. Like, what's everybody else missing and why?
Because from my point of view...well, okay, let me go back.
So, February 2020 — mid-ish February 2020, late February 2020 — I had a course coming up at the University of San Francisco that I was going to be teaching. I had heard increasing chatter about this Chinese virus thing.
What then happened was it hit Italy, and there was a lot more information in English about what was happening in Italy, than there was what was happening in China. So it suddenly was much more accessible to see what was going on, particularly because a lot of the Italian doctors were actually on Twitter and stuff, so you could read what was happening.
A whole bunch of people were saying like, "This is a disaster", "The president of the Italian medical body just died of COVID," and, "There's not enough hospital beds." I knew it had kind of just started to get detected in New York.
I thought, "Oh, well, it seems like it might be quite likely to come here. What does that mean for our course?" Not at all altruistic. Just, like, are we still going to do our course?
My wife and I kind of started reading about it to try to figure out what should happen with the course. And as we did, we were...yeah it was  very obvious that it was going to be a global pandemic and it was going to sweep through San Francisco within weeks. And so like within two days, I wrote an email to everybody who had registered to the course, and put out a blog post, and said we're not doing the course live. We're going to do it virtually.
This is well before our university — or I think any university — had decided to do that. Which again, I already thought was weird. Like I thought, "Okay, it's not yet here, but obviously it's going to be. So why are people acting as if it's not going to be?"
Rachel and I ended up writing a long blog post. We were kind of like, "Okay, it's not just our course." We've got all these friends in San Francisco who are doing things that we're pretty sure they're going to look back on in hindsight and think, "That's a terrible idea, because I put myself and my community at risk."
So we said...we didn't know much about it, so we just said, "Look, as data scientists, here's what we can see so far in the data. It does seem to grow exponentially, at least at first. And, you know, this is the impact it's been having in Lombardi. Here's the early impact in New York. Here's how the math of these kinds of things work. Here's not just a prediction, but an almost certainty as to what's going to happen here."
That got a lot of attention. We had no idea how to avoid it ourselves. We were worried that...historically, when there is global pandemics, it can lead to violence. It can lead to societal disharmony, or whatever. We decided to get out of San Francisco for a while.
We also...it was clear that there was going to be a lockdown at some point because, I mean, why wouldn't there be?
Again, none of our friends seemed to believe any of this is going to happen. It's really...I thought it was weird, it just seemed very obvious. And then yeah, there was a lockdown like a week or two later.
We had told our daughter's school, "Oh, there's probably going to be a lockdown." They sent back this rather annoyed email about interrupting learning or something. The schools were closed for a year in the end, in San Francisco.
Then we were like, "How do we not get COVID?" Because we probably don't want to get COVID, because it seems like getting COVID can be bad. We started to hear from people who would like...saying maybe there could be longer-term implications of some of these kinds of SARS viruses.
So I started looking into how it spread, and I discovered that there's all these countries around China that had avoided getting hit by COVID. Particularly Hong Kong, that's literally a train line away from Wuhan. And that just seemed amazing, you know.
That's when I discovered that Mongolia, Taiwan, and Hong Kong all had this either universal mask policy or universal mask usage, kind of culturally. And I thought, "Oh, that's weird." Because I thought masks were this kind of weird thing. For some reason, you go to Chinatown, you see people wearing masks and that's how it's is, and that's weird. I didn't give much notice of it.
But then I started learning it was this respiratory infection, and it kind of started to make sense. I wrote something in the Washington Post talking about how in the Czech Republic, particularly, the populace had independently decided to wear masks, heavily driven by a popular science YouTuber.
Basically, within like three or four days, the whole country had made enough masks for everybody, and their president was talking about how proud he was. Again, their infection was going the opposite direction to other countries, I thought that was interesting. So yeah, I kind of wrote an article about that.
I talked to a guy who used to be very high up in the government on the science policy side, and I asked him what's going on with masks. He said like, "Well, nobody thinks there's very convincing science about it." He said if you want to convince people to wear masks, then you need to find some better science.
So I contacted basically the 18 smartest scientific researchers I knew, everybody from Lex Fridman to Zeynep Tufekci and said — not just scientific researchers, in Zeynep's case a sociological researcher — and said like, "Do you want to help me put together the evidence?" That's where our paper came from.
Basically, everybody said yes, they all agreed.
Suddenly we had this huge author group, so we kind of set up a Slack channel. None of us had a really strong opinion going in. Had one of the world's best aerosol scientists, he was probably the strongest opinion going in because this is his job. He was like, "Well, let me explain aerosols to you."
Then what happened was there was this amazing couple of papers that actually used this laser-scattering light chamber thing to actually literally take videos of respiratory particles suspended in the air. Not suspended, but they just float in the air. It showed that they float in the air for up to an hour. And it showed that when somebody wears a mask, they don't appear.
That was the point where I went from "curious and interested" to "100% convinced".
Because it'd be like if somebody said, "I promise you, Lukas, if you throw this ball at that wall, it won't bounce off. It will go through." You'd be like, "Well, Jeremy, I'm not sure. But I'll give it a go." And you throw the ball at the wall, and it bounces off, and you go like, "Jeremy, I am very sure you're wrong about your theorem."
And that's how it was with masks.
There were people who said masks don't provide respiratory protection from these airborne particles, and then here's a video of them not going through the mask. I was like, "Okay, that's...I don't need any RCTs. There's a video. There's a picture of it working."
I kind of went all in on just trying to say to people, "No, there's actually a thing that stops the thing that infects us. So we should wear them." I found it extraordinarily bizarre that everybody didn't just go, "Oh, look at that video of it working. Therefore, it works."
It was a super frustrating experience. I don't...there's nothing I enjoy about researching masks and there's nothing I enjoy about political advocacy. The former is boring and the latter is stressful. But when there's something that so obviously can save millions of lives — and also can avoid who knows what long-term harm — it just seems absolutely ethically required to act on that. 
I spoke with all kinds of world leaders, and politicians, and celebrities, and whatever. In every jurisdiction, it was like a whole new conversation. It was like, "Talk to people in South Africa; 'Oh, we don't believe in masks.'" It was like, "Talk to people in London; 'we don't believe in masks'. Talk to people in Australia; 'we don't believe in masks'. Talk to people in Florida; 'we don't believe in masks.'"
Each one, I discovered this horrible thing. Which is everybody decided they didn't believe in masks until their personal jurisdiction got hit hard by COVID. Wntil the hospital started filling up. And then they would get back to me and say like, "Oh, tell me more about this mask thing, Jeremy."
That was infuriating because of course the answer is, "Well, if you had put in mask mandates two months ago, then this wouldn't have happened. Now it's too late because masks can reduce R by a bit, but not enough to reverse a full-on pandemic, once it's there."
Honestly, it...I got really burned out by the process. In some ways it was successful, but in the end, the pandemic still happened. And in the end, I'm still flabbergasted, particularly now that high-quality medical masks are widely available. Demand is so low that factories have been shutting down.
I've never had COVID. Literally nobody I know who has worn a high-quality mask at all times indoors, none of them have got COVID. And everybody I know who doesn't, have all had COVID.
There's a point at which you kind of say, "Okay, I've done what I can. You do you."

Lukas:
So you continue to wear a mask indoors, at all times?

Jeremy:
Of course. Yeah.

Lukas:
What would change...when would you stop wearing a mask indoors?

Jeremy:
I suspect it's the same as the answer to the question, "When would I stop drinking clean water?" I'd rather keep drinking clean water.
We decided...I mean, remember, it took decades — even after the John Snow experiment — for big cities to decide to invest in clean water infrastructure. Presumably after some number of years, we will invest in clear air infrastructure.
China's already done it. They now have, I believe, HEPA filters in pretty much all their public buildings, and they're putting in UV sterilization in pretty much all their public buildings.
Hopefully, at some point, the West will do the same thing and then it'll be like, "Okay, I'm in an environment with clean air," so I don't have to self-clean the air.
That'd be one option. Another would be...again, China's ahead of us on this. They have nasal vaccines, which are probably much more effective. If we eventually get those, I think they can actually make a significant dent on transmission. The injected vaccines don't make much of a big impact on transmission.
So yeah, there are technologies that should allow us to be able to be pretty safe in indoor spaces.

Lukas:
But you don't wear masks in an outdoor space? Is that the...

Jeremy:
No, I mean, it's not exactly a hard and fast rule.
We went to a birthday party recently, for example, where it was a karaoke thing. It was outdoors, but all the kids were singing, and they were tightly packed, and whatever. So, our family wore a mask because there's a high amount of aerosolizing activities going on with a high density of people.
But yeah, broadly speaking, I'm not too concerned about outdoors because the airborne particles disperse much more quickly.

Lukas:
I see.
I guess the interesting thing about that story maybe is that there maybe was a fairly broad scientific consensus, but no one was really ready to advocate for it. Is that a better summary of what was happening?
If you got all these scientists together and they actually all agreed with what you were saying...

Jeremy:
They didn't, unfortunately.
What happened was it was highly polarized by areas. The people that actually understood this are the aerosol scientists. And the aerosol science community was basically 100% all on the same page. Like, "Talking, breathing, these are aerosolizing activities. We have loads of evidence that this is transmitted through aerosols. We have loads of evidence that in the droplet nuclei — that are suspended in the air — masks block those from getting to your lungs."
All those were pretty much understood in that community. But then the challenge is, Lukas, that we haven't had a major respiratory pandemic in the West, really, since the Spanish flu. So, none of our infectious disease community has any background in that.
I spent a lot of time advocating — including speaking directly to the WHO's infection control groups, the folks who kind of ran the response at the WHO — and they were overwhelmingly people who had a background in infectious diseases that was bred through contact.
The kind of stuff that hand washing helps with. So they were just coming from a totally different direction, and had decades of experience on treating different kinds of diseases in a different way.
They were doing their best to learn and understand. But for some, that was a very difficult experience. One in particular, John Conly, his financial stake was very high in this fomite transfer. That transmission is not through the air, but by contact, because he has financial interests in that being the case. So, very difficult for him to come to terms with the idea that this is a respiratory infection, through respiratory particles, requiring respiratory protection.
That was a big challenge, this worldview difference between different scientific groups. The aerosol scientists, there were actually none of them on the WHO's infection protection committee...infection control, whatever it was.
I noticed — when I was talking to WHO — it was a total lack of diversity. Every single one had the same kind of academic background, and the same way of thinking about things, and they all knew each other very well.
They were also...being involved in the WHO is a very strong status signal in their career, so everybody wants to be invited to those kinds of things. And so you really want to have all the other people on the committee think you're a good, nice person. It creates this real monoculture. So that was another big part of the problem.
It was all...it definitely made me a lot more cynical than I was before it, to see how the WHO works. And even our big paper, how to get it published. It took a year from being written to being published.
By the time it was published, it was basically too late. The process of getting it published was much more about politics than about science, you know.
It was disappointing for me to discover that systems that I had thought of as being very much focused on rationality and data and correctness and rigor...so much of it turned out to be about politics, and networks, and stuff. I guess I was probably pretty naive before all that happened.

Lukas:
My sense is that people broadly believe that masks reduce the spread of COVID at this point. I'm not sure that I know exactly to what degree...it sounds like you're saying to a really massive degree. 
But I think you had a part in that. Or maybe just...I just follow you on Twitter and we were just watching you talk about it. But I don't know. It does seem like it’s the mainstream...

Jeremy:
Yeah, I mean, I was leading the Masks4All group globally. We were the most substantive group doing that. Absolutely.

Lukas:
It feels like it was successful, though. I mean, I just...do you not...

Jeremy:
It was successful-ish.
If you're in San Francisco, it'll look more successful than if you're in Australia, for example. In Australia...from time to time, we've had mask mandates and everybody wears them when they're told to. The rest of the time, it's strongly recommended, but nobody does. But in San Francisco, I'm told maybe 30% of kids at schools — or some schools — are wearing them.
It's definitely...it's disappearing. And also people — a lot of people, maybe most people — I see wearing masks, at least in Australia, are wearing masks that don't work very well, even though the good masks are really easy to get.
And a lot of people don't realize like if you get a high quality N95 respirator, you could wear that as many times as you like, until the straps wear out. A lot of people think, "Oh, you can only wear it once." A lot of people think it has to be fit-tested. A lot of people think it's like donning and doffing is some complicated thing.
There's all this wrong information out there. And so the number of people actually wearing high-quality masks is...to me, it's surprisingly low. If everybody wore one whenever they were indoors, I think we might...particularly if we also had HEPA filters in indoor spaces, I suspect we would be done with a virus, that it would go away. Because how would a respiratory virus continue to transmit when you break the flow of respiratory particles?
Yeah. I mean, even in China. All the pictures I see, everybody's wearing surgical masks. It's, like, weird to me.


Researching how to improve children's education
Lukas:
Interesting.
Well, look, we're almost out of a time and we always end with two questions. But you're a little bit of an unusual guest, I don't know exactly how all these will fit your worldview. We like to...I like to ask people, if you had some extra time to research something completely different, what might it be?
I feel like you are just an unending font of this stuff. What are some things that you're interested in that you haven't had time to look into?

Jeremy:
Well, I'll answer a slightly different question because any time I'm interested in researching something, I just do.

Lukas:
Fair enough.

Jeremy:
The most recent thing I spent a lot of time researching is children's education.
Our daughter missed the first year of school. Because of COVID, in San Francisco they were closed. That would have been her kind of transitional kindergarten year, as they call it in California.
Then we came to Australia, and so she went to school — regular school — for the first year here. She was straight into grade one. She enjoyed it. She was always happy to go, and happy to stay there.
But it felt like she had blossomed a lot more during her previous year when she was doing stuff over Zoom, and on apps, and stuff than the year that she was in-person in the classroom, which really surprised me.
Instead, she had become much more of a perfectionist and was becoming much less resilient after her year at physical school. That all seemed really weird to me, because I thought that environment would be much more healthy than the previous one.
I started investigating it really carefully and studying a lot of academic papers about education. I was stunned to discover that there's pretty broad consensus in parts of the academic community — or some very strong data — that suggests schools are not a particularly great place for most kids to really blossom, or at least entirely focus on school learning.
In fact, tutoring...kids who get tutoring are in the very top, highest academic performers regardless of their previous background. It seems like all kids can be really successful given the right tutoring.
Our daughter was doing all this stuff with apps, and on Zoom, and stuff during her first year. None of that is limited by the speed at which a teacher thinks a kid should go, but instead the computer is dynamically adjusting difficulty over time. So, weirdly enough, our daughter was basically at Grade 4 or Grade 5 of math after a few months of doing these apps. They're so much more effective than normal teaching.
We were also trying to figure out, "Well, how do you avoid her getting really bored and stuff?" So I did this really deep dive into education and discovered there's all these fascinating, different ways of teaching and learning which are entirely different to what's done at normal schools.
Eventually, we decided to take her out of school and instead switch to using these kind of more academically driven approaches in a homeschooling environment. Which also seemed to generally lead to better social outcomes, better mental outcomes — better mental health outcomes — and better learning outcomes.
That's kind of been interesting to me, to discover this whole world of research that seems really important, for humanity. How kids should learn. It feels like, again, it's being largely ignored by the institutions that we send our kids to.

Lukas:
Let me just see if I got the summary of this: basically that tutors are much more effective than schools at actually teaching kids things. Is that what you’re saying?

Jeremy:
That would be part of it. But there's lots of...that's kind of one starting point. Yes, even kids that would otherwise have been doing pretty badly at school can be in the very top performers. That kind of is an existence proof, that pretty much all kids can be extremely successful.
But then there's also this kind of interesting data point for us, which is when we gave our daughter an iPad, and some math and reading apps, and somebody on the other end of a Zoom to supervise them, she had a huge amount of fun and learned dramatically more quickly than I thought was possible. And then when she actually went to school, she basically learned nothing for the whole year and ended up becoming much less resilient.
There are specific ways of learning that are not particularly compatible with the normal ways we teach at school.
For example, we might have talked before about Anki and repetitive spaced learning. My daughter does Anki every day. Literally everything she learns, she will remember forever if she creates a card for it, or she decides she wants to know it.
That's kind of quite difficult to do at a normal school because you'd need all of your grade levels to be doing Anki. So that in Grade 5, you've still got cards from Grade 1 or Grade 2 coming back.
But what happens at school is each year...for example in Australia, the Year 7 and Year 8 math curriculums are nearly entirely a refresh of the primary school curriculum, because they kind of assume the kids are going to need to see it again, because they've probably forgotten a lot of it.
Things like, "How would you incorporate spaced repetitive learning?" Some schools in England have tried to do something like that using something they call "retrieval practice". I know there's a school called the Michaela school, which I believe had the highest results academically in the whole country. They do something like this.
There's a few...there's a handful of schools here and there which are trying to use these kind of research results. But they're kind of the odd ones out.


The importance of executive buy-in
Lukas:
All right.
Finally...I don't know if this one really applies to you. We usually ask — because my company, and this interview, is all about making machine learning really work in the real world — we usually ask like what's a hard part that you've encountered in taking something from research to actually working for some purpose?
That may not exactly apply to you, but you seem very good at sort of interpreting my questions in a useful way. So I pose it in its most abstract form.

Jeremy:
I mean, I've had lots of projects that I've tried to bring into the real world.

Lukas:
Of course, that's right. Yeah.

Jeremy:
It's difficult.
I've been doing machine learning projects for over 25 years now, believe it or not. In the early days, it was such a challenge because managers didn't believe in the power of data at all.
When I would try to tell them that it could be really valuable, they would always say like, "Can you point to a role model of a company that's been successful because of their use of data?" And there were none. That was tough.

Lukas:
Yeah.

Jeremy:
Then Google came along, which was great, because then I could point at this one company that was really working hard to use data and they've become very valuable because of it.
Nowadays that bit's a lot easier. But actually, unfortunately, my answer is going to be that I've kind of — for a lot of companies — I've given up on even trying.
Because I tried to get...particularly when I was at Singularity University, where all of our students were basically execs from giant companies. We were trying to convince them to be more data-focused and some of them really took that on board. And then they would invite me to come and talk to their VP groups and exec groups.
I saw lots of big companies try to get more data-driven, try to use machine learning. I didn't see any being successful. The issue seemed to be that their entire management teams were people who...that was not their area of expertise. They were not promoted because they were good at that.
They would have very smart, data-driven people down in their kind of business analyst levels, that they would have no idea which ones knew what they were talking about, and have no way to kind of curate what they were being told. All of the promotion systems were based on experience, and credentialing, and things other than analytical capabilities.
So, in those kinds of companies, I eventually decided, "Okay, maybe it's not possible for a legacy company to become a data-driven company." And so nowadays I focus all of my attention on startups created by founders that are already data-driven and have a good understanding of analysis.
What we're seeing is, increasingly, the most valuable companies — or particularly the most valuable companies in America — they're basically all now "tech startups". I mean, they're not startups anymore, but they're all companies that are created by engineers and data-driven people.
I think for data scientists interested in making an impact, the best thing to do would be to try and make sure you're at a company where that kind of work is appreciated and understood by the executive team.


Outro
Lukas:
Interesting.
Well, great to talk to you. That was super fun. Thanks for-

Jeremy:
You too, Lukas.

Lukas:
-answering my wide range of questions. It's always so inspiring to talk to you. I really appreciate it.
If you're enjoying these interviews and you want to learn more, please click on the link to the show notes in the description where you can find links to all the papers that are mentioned, supplemental material and a transcription that we work really hard to produce. So check it out.


Bonus: Weights & Biases
Jeremy:
And how is everything going at Weights & Biases? I always hear nothing but good things about it. Everybody loves it.
I've got to admit, actually, the other day I was talking to my friend — I think it was Tanishq — about like, "Oh, what's going on with this learning rate here? I wonder if it's working properly." And then he's like, "Well, here's a graph of the learning rate."
I was like, "Oh, that was quick and great. Where did that come from?" He's like, "Weights & Biases, it logs it."

Lukas:
Yes! Oh, man. Are we still recording? Put that on the...

Jeremy:
I probably should have looked at the Weights & Biases team. Here I was with like "plot.plot(x = ...)", and he's already got it pasted into the Discord chat.

Lukas:
All right. Well, that made my day. Thanks. 

Jeremy:
Cheers, mate. 

