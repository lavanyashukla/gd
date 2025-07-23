Shreya Shankar — Operationalizing Machine Learning
Shreya explains the high-level findings of "Operationalizing Machine Learning: An Interview Study", an interview study on deploying and maintaining ML pipelines in production.

Timestamps
0:00 Intro
0:53 Shreya's background in industry and academia
8:59 Findings from "Operationalizing Machine Learning"
19:05 Examples of data challenges in production
27:13 Shreya's thoughts on Jupyter Notebooks
34:14 Shreya's thoughts on ML tooling
40:42 ML tooling layers, tech stacks, and workflows
51:33 Provenance and evaluating different solutions
54:12 Outro

Transcript

Intro
Shreya:
We found that the velocity really matters a lot. The ability to validate as early as possible matters a lot. You don’t want to push a bad model to production. You don’t want to wait until your final stage of A/B testing, in order to find out that something is not going to work well.
So we found that the earlier you can validate, the better it is.

Lukas:
You're listening to Gradient Dissent, a show about machine learning in the real world. I'm your host, Lukas Biewald.
Shreya Shankar was an ML researcher at Google Brain, and an ML engineer at Viaduct.ai, and now she's a grad student at UC Berkeley where she wrote a paper that we all love here at Weights & Biases called "Operationalizing Machine Learning: An Interview Study".
This is a really fun interview. I hope you enjoy it. 


Shreya's background in industry and academia
Lukas:
All right. Thanks so much for doing this. I really appreciate it. 

Shreya:
Of course. Thanks for having me. I'm excited. 

Lukas:
I think we've all been watching you on Twitter — or following you on Twitter — for a long time, so it's exciting to meet you.

Shreya:
You know, it's funny how every now and then you run into a Twitter mutual or whatever and it's like, "Oh, I know you, but I don't really know you. But I know you."

Lukas:
Totally. We were actually doing a podcast with Sarah from Amplify Partners and we both started talking about how much we liked your paper and I was thinking, really, I should just go directly to the source.

Shreya:
That's so funny.

Lukas:
But yeah, maybe if you could tell us...before we get into your paper — which I really want to talk to in-depth — maybe if you could tell us a little bit about your career and how you got excited about operationalizing machine learning. 

Shreya:
Yeah. It's such a buzzword and, honestly, not the most exciting thing in the world. So it's kind of weird to think how I got here.
I started out kind of doing deep learning research, ML research in adversarial examples, because that was the hot stuff in 2016, 2017. I had this moment of crisis when I graduated college. Should I do a PhD, or should I go and be an engineer, or go into industry?
I decided, okay, I might as well go into industry, because I'm trying to write my statement of purpose on working on robustness in machine learning systems and ML system deployment, but I didn't really know what any of those words meant, because I had no experience. So I went to a company — I went to a startup that was doing applied machine learning — and I was there for a couple of years.
That kind of changed the course of what I believe to be some of the most pressing problems in operationalizing, I guess, these ML systems. It's a very broad topic. I define it as anything that requires having a machine learning system that's serving some output that people use on a regular basis, that you don't want to shut down.
I think that's just a completely different ball game than just the ML research that I worked with. And there's a lot of problems in there, both technically and organizationally, like the processes people use to...like, on-call processes. Things that people do to ensure reliability of their systems. And then of course the tools, the principles, and techniques.
I found myself really going back to the databases and data management world in terms of like, "How do I create these systems so that a bunch of data scientists can train models?"
And that really led me to, I think, doing a PhD in databases, where a lot of these problems — a lot of these MLOps problems — can be recasted as traditional data management problems. 

Lukas:
Interesting. 
Going back to when you got your first job...we hear about this a lot, but what were the biggest surprises about machine learning in practice versus studying machine learning in school? 

Shreya:
I think I had a nice trajectory of surprises, because I started out kind of as the first ML engineer, and then we grew like 8x, 9x in my time at the company. We hired more ML engineers and more data scientists.
My first surprise was that training the model itself — that whole experimentation to first model — is a process that you don't want to replicate with as much human labor as you do in the initial experimental stage.
When you deploy it — that retraining, that kind of component — you kind of zoom out on your entire pipeline. You want to automate that so your human attention doesn't go there. It's, "How do you glue together that model in relation to all of the other stuff you have?"
That was one nice realization that I had. And then after that, I stopped spending so much energy and time modeling itself for the sake of modeling.
Another realization that I had was, when you have multiple data scientists working on the same kind of model — or prediction task, or pipeline, or whatever you want to call it — all of a sudden, you need some sort of processes to make sure everyone is on the same page.
If I try some sort of experiment, or I have this domain expertise around, "Hey, the set of features probably won't work well. Or, this source of data is corrupted, so don't try to make features from that," how do I share this knowledge in a way that's not a stream of thoughts on Slack?
And how do I keep this up-to-date as people come and leave the team? That happened a lot at my previous company before grad school.
There's a lot of these small, small problems that kind of built as we grew organizationally. As well as grew in terms of the number of customers we were serving, the number of ML applications we were delivering, or predictions we were kind of serving to different people.
Yeah, there's so much. I don't know how to give you a succint answer to that. 

Lukas:
It's funny because you've also had the opposite experience here, right? Everybody talks about the shock of going from academia into industry, but you actually went from industry back into academia.
Were there any surprises or misconceptions that you saw going back into the academic world? 

Shreya:
I think it's different for me because I also switched fields. Databases have been...okay, machine learning has also been around for a long time, but the kind of venues that have been popular in databases have been around for a while.
The norms are a little bit more well-defined and they're not changing as rapidly as the ML research norms. The community isn't growing at the scale that ML research is growing. In that sense, I felt like I was kind of walking into a completely different territory.
I think...what I really like about the database community is they're very open and accepting of new ideas and new paradigm shifts. And I think it's because they've seen it multiple times before.
They've seen it, like SQL to unstructured data, or structured to unstructured data. They've seen it from transactional systems to OLAP systems. They've seen Webcale, all sorts of stuff. Like the MapReduce era. Maybe that's still going, I don't really know.
In that sense, I think they're very eager and receptive to work in this kind of ML systems or data management for ML space. Which I felt that, at traditional ML venues, it was almost like you need to train models in order to have your papers accepted. If you weren't training models or doing model inference, then is this a research paper?
I don't know. I think database is just a better home for the work that I'm doing. Not to diss on all the model training work, of course. 

Lukas:
Why is that? Because you care about practical, real-world applications. Is that a good summary? Or, why does database...

Shreya:
Yeah, there's a lot of problems around operationalizing models that are data management problems. When you do research in that, what venues are going to accept that research?
I'm not necessarily training models in this research. So it's less likely, I think, for ML than [?] to accept this work. I'm also borrowing a lot of ideas from databases around how I think of models, how I think of provenance, how this can be used to solve a lot of observability problems. Things like that.


Findings from "Operationalizing Machine Learning"
Lukas:
Well, so then you wrote this really fantastic paper, which we'll definitely link to. I was almost thinking maybe we should make a required reading before listening to this podcast where you get into details.
You wrote this paper on operationalizing machine learning. And you went out and interviewed a whole bunch of practitioners and summarized the field. Which is something that I always try to do, I almost feel like this podcast could be called "Operationalizing Machine Learning".
I thought you really put things in a really well-structured, really interesting [way], and surprising results that showed that you were really getting deep with the people you're interviewing.
But I guess before we get into it, could you maybe summarize the key findings of the paper — for the folks that haven't read it — and then we can dive into the nitty gritty?

Shreya:
Sure. So, we interviewed around 20 practitioners. The criteria was that they have worked on — or are working on — a model that's being used in production. Basically, it's serving some predictions or some output that customers are using, and somebody will get an alert if the system breaks. That's kind of our definition of production.
We interviewed people across company sizes and across applications like self-driving cars, banking, whatsoever. We found...we looked for common patterns across people's interviews. 
We found four high-level stages of their workflow around experimentation, like the evaluation and deployment, monitoring and response. And then data collection, which wasn't often performed by the ML engineers that we interviewed, but it was a critical part of the production ML pipeline.
We identified these four components — or these four stages — and then we also identified, "What are the variables that govern how successful their deployments will be?"
Like, "What are the things to think about whenever evaluating tools to use in each of these stages? How do I know if I'm on the right track to a successful deployment?"
And we found that the velocity really matters a lot. The ability to validate as early as possible matters a lot. You don't want to push a bad model to production. You don't want to wait until your final stage of A/B testing, in order to find out that something is not going to work well.
So we found that the earlier you can validate, the better it is.
And then finally, the last "V" is versioning. Which is, "How do you manage all of the different versions of models that you're going to have as time goes to infinity? How do you think about all the edge cases or corner cases that your system must respond to?"
Maybe that's slapping on a different version, "If you come from this customer, or you come from this population, we'll give you this version."
Managing that is a pain point. So that's the high-level findings.

Lukas:
You obviously have a fair amount of experience in this already, having done this job yourself. And you're pretty active on Twitter, and have been in the conversation around this for quite a while. Were there parts of what you heard that surprised you? 

Shreya:
Definitely. 
And selfishly, I think, I conducted this study so thoroughly and as a research thing that took 1.5 years that we kind of did on the side. I did this because I was so afraid that I was leaving industry and going into academia, and I'm going to go into a bubble, and try to build systems for people and not know what I'm doing, or whether this is useful.
What I did not expect was to kind of change my research agenda and direction. One concrete example of this is distribution shift. I used to believe...well, this maybe is a problem depending on how you define it.
But the idea that if you have this static model in production — a static set of parameters or a function that's being called on some features, and these features are changing, time is going on — at some point, you're...this is like the classic "view staleness" problem in databases, right?
You need to refresh your views to keep up to date with the underlying data. If you think of a model as a view on a table, the same thing exists.
But I think a lot of the ML literature — or even things that I'd been thinking about are, "How do I make my views robust to these changes in the underlying distribution?" In practice, "Sure, that's great," but if something as simple as recomputing the view or retraining the model solves my problem of staleness, then why don't I just do that?
You'll find that at these very large organizations like Meta, Google, Amazon, et cetera, that they're simply retraining their models like six, seven, eight times a day or even every hour. And distribution shift is not their problem.
In this setting — when you're retraining all the time — retraining on corrupted data becomes a problem. "How do I make sure that my data is clean and uncorrupted? How do I identify when to block a retrained model from being promoted back to production?"
All these sorts of problems...it's like, oh, these are very interesting research problems, but this is not what I thought of distribution shift to be.
Hopefully that answers your question. I can think of others. 

Lukas:
Totally.
The people that you were talking to, were they like individual contributors building models or more like managers? We often see like a separate MLOps team that's sort of doing the infrastructure, while other people are kind of doing the training.
Who were the kind of folks that ended up in your study? 

Shreya:
We required that everyone was an ML engineer — responsible for a model, or pinged when the model predictions are bad or someone's complaining — at some point in their career. Some of them had switched to the infrastructure-building side. Some of them had become manage...I think two of them had become managers. That's written in the paper.
Everyone there acutely knew what it was like to have put a model in production and somebody complained about the predictions. That's really what we wanted to drill into. Like "All right. What did you do to fix this? What does your team do to fix this?"
Simply retraining the model often fixes it, like 80% of the time. These ML engineers have so much on their backlog. If they can kick off a retrain, and get to something else on the backlog, and it works 80% of the time, that is going to be the solution. That is the best solution.
I feel like more ML researchers should know this. But it could be...maybe I'm biased.

Lukas:
Were these people mostly doing unstructured data? One of the big dichotomies that we see is structured versus unstructured. Where unstructured, you often get more neural net techniques, you get bigger models. You get almost a totally different stack in many cases.
Did you observe that too?

Shreya:
Definitely, we talked to some people who had very image-heavy...self-driving cars or autonomous vehicles was a good example of this.

Lukas:
For sure.

Shreya:
They're definitely using neural networks.
I think when drilling, though, into data quality and this kind of data management, I think people tend to think about relational data management. "How do I manage the embeddings?" or "How do I manage tuples?"
I don't know if we've gotten to the place where we're thinking about traditional data cleaning and data quality, in terms of images or other unstructured data. We didn't focus the interviews too much on that.

Lukas:
Were people doing a lot of exploration of features? Did feature stores show up much in your interviews?

Shreya:
We explicitly went into this not wanting to hit the buzzwords, just to see what buzzwords would come out.

Lukas:
Totally.

Shreya:
Feature stores were almost never mentioned.

Lukas:
Interesting. Why do you think that is?

Shreya:
I think people thought about the idea of a feature table or a feature service, but very few people said the term "feature store". What mattered to them was just having features that were available for them to query.
Oftentimes at organizations, it just happens to be a cron job that's populating features in...obviously, not at Meta, they're not going to have a Postgres table of features. But in a lot of mid-size cases, mid-size companies, where you can have Postgres table with features, and you can have a cron job that recomputes features every day, and it's fine.
I think it ends up going back to this view staleness problem. How stale does it need to get for your business to experience some performance hit? I don't know if you need to be computing them on-demand all the time.


Examples of data challenges in production
Lukas:
I love your simple categorization of data collection, experimentation, evaluation, and monitoring, and response. Did it feel like...of those categories, I think you said data collection was usually a different team.
Where were your respondents spending most of their time, and where do you think they felt the most pain was?

Shreya:
Because all of the pipelines that they talked about were deployed or already in production, people did not focus on experimentation as much.
I imagine that this is not representative of the ML community at large. I think there's a lot of people who are still working on getting their first production pipeline out there.

Lukas:
Just to be clear, none of these questions are leading. We're not...

Shreya:
Yeah, I just want to say this is definitely a biased subset towards production pipelines. I think the evaluation and deployment...actually, I think monitoring and response...
It's hard. 50/50 on those, just based on the annotations of the interviews that we did. Or the codes and how we grouped them. It was very 50/50 on those two.
And they often link into each other. People will talk about problems with monitoring stage deployments. Does that fit in monitoring or stage deployments? I don't really know, but I think it's definitely a big pain point. Evaluation and beyond.

Lukas:
One of the key findings here is that monitoring for data corruption or catastrophic errors is more important than monitoring for data drift.

Shreya:
Totally.

Lukas:
But you'd sort of imagine that monitoring for data corruption would actually be a lot simpler. What makes that so challenging to do in production?

Shreya:
I'm writing a paper on this, based on some work with Meta.
In the limit, people may add features to a model. They don't remove features. What happens with these models ends up getting hundreds of features, to thousands of features, to ten thousand features. That's one thing. You've got models in production with tens of thousands of features.
Another thing is that people are coming and going in these organizations. The ML engineer who built the model does not exist at the company anymore, and the model is still in production.
Couple that with existing data monitoring or data cleaning solutions — which is, defining schemas for all of my features. Like bounds, acceptable values, types for each one of them — great. Who is going to do that and maintain that as these feature tables or as these pipelines evolve? I don't know.
The other thing is, because you have so many features, the probability that at least one record and one column is corrupted is so high.
And then you get this problem we talked about in this paper, of just straight alert fatigue. It's so painful. At the end of the day, it doesn't matter if just a couple of records are corrupted in one column.
The problem is, again, when does it get so bad that it brings down the business? And how do I find that pretty precisely?

Lukas:
It's funny. I'm nodding — I've lived this myself, many, many times. That's why I totally agree — but I'm actually thinking if I hadn't lived it, it might not be obvious how this happens.
Is there a concrete story you could tell, about how a feature gets corrupted in production and the havoc that it causes?

Shreya:
Yeah. Okay. I want to give...I feel like this is a question where people will attack me for any answer. If I give an example of a Meta or a Google, they'll be like, "Oh, but not every company is a large company."

Lukas:
I think the story just illustrates the chain of events. Of course we're all so smart that we never have bugs, but...

Shreya:
Sure. I think I'll give one example at my previous company, which I lived.
Features were generated from different sources. When I say different sources, it's not just weather data or whatever, it's like, different clients have different data. And then also, we have different data pipelines that are repeatedly pulling from Snowflake or repeatedly generating features.
Oftentimes these pipelines will fail, because maybe there isn't enough resources or there weren't spot resources available in us-west. I don't know. Things will happen and these things will all be null.
Will this corrupt model perform significantly, to where I actually see a regression? I don't know. But this happens a lot.
It also happens that some of my clients, they send me data every day. One day, they send it in a CSV or Parquet. One day, they switch the order of the columns. A totally reasonable thing, but again, impacts a subset of tuples, a subset of columns.
I could name a bunch of these. I think this is pretty generalizable to most orgs.

Lukas:
Totally.
I remember at my first job, all the features — for some reason, there's no technical reason this is necessary — but someone started just naming each feature column with four letters — literally four letters — for no reason.
We just kept doing it, so all the feature names were just a really compressed word.

Shreya:
Yeah, stuff like that-

Lukas:
At some point, no one knew what they meant. It was nuts.

Shreya:
Stuff like that really just makes it so hard to go back and trace these bugs.
Why did my model regress 2%, for example? Oh my God. There can be a laundry list of reasons why. Just to even go there and try to investigate why would be a nightmare.

Lukas:
I guess, though, if the people you talk to are just constantly retraining over and over, that actually might be one way to avoid data corruption. Provided the way that they collect the features is the same as how the features get loaded into the model in production.

Shreya:
Yes and no.
Suppose I retrain every hour, and when I retrain, I just fine-tune my model on the last hour's data. I split that into training, retraining, and then I split a little bit of that into validation. My criteria for passing is it has achieved reasonable performance on that small validation set.
Suppose that whole hour of data is corrupted. It might just be the case that, "Great, on this corrupted data...because I trained on it, I performed well on the validation set. Amazing. Same distribution."
Put it back in production, and then somebody fixes the bug, and all of a sudden the performance changes. Because that snapshot of data was different from previous snapshots, or future snapshots.

Lukas:
Right, right.

Shreya:
I do think that there is this still data corruption problem.
The challenge is in identifying the corruptions at the timescale that engineers react and respond to bugs. So you don't put models in production that won't do well on future data.


Shreya's thoughts on Jupyter Notebooks and ML tools
Lukas:
I guess one of the little gems in your paper is the controversy...I forget exactly how you put it. You said Jupyter Notebooks are quite controversial, or quite a "bimodal distribution" of responses on that.
I'm kind of curious your take on Jupyter Notebooks.

Shreya:
I think my take is a little bit biased. I'm not old enough to have lived the history of data management tools, like spreadsheets and whatnot, when they came out.
But from my reading of old work, it seems that these quick and dirty prototyping data tools were used to tell stories, and have primarily been used to tell stories, regardless of whether it was done correctly or not. I think that this is the case for a lot of data tools. Jupyter Notebooks are not really an exception.
While...if I want to start a company around my opinionated..."I don't want errors and I want...No one's allowed to use Jupyter Notebooks," I think that's just an opinion.
I feel like it's completely useless to go and try to prescribe a philosophy to a industry that has a pattern of using these data measurement tools.

Lukas:
That's kind of interesting, because I actually feel like you're putting yourself in a place where lots of people might come to you and be like, "Shreya, what should I..."
People come to me all the time, and I think you're more qualified to say, "How should I set things up? Should I be letting my team use Jupyter Notebooks?" And I guess if someone asked you...am I hearing you right that your answer would be, "No, don't use Jupyter Notebooks"?

Shreya:
Oh, gosh. I think it really depends on the application, or what company I'm trying to run, or what team I'm trying to do. What are the engineering predispositions of the people on the team?

Lukas:
Man, you're turning into such an academic. I love it.

Shreya:
I'm sorry. I can't give... But I think that's the point.
One thing about this paper is that it's an academic paper, so we can't write all of our opinions in there. But I really wanted to drive home the point where it's just like, the reason that we think that people have these conflicting opinions is because they have conflicting priorities.
Do they want initial velocity to be a higher priority than validation? That's personal. Or, that's organizational. I think those values are different for everyone.

Lukas:
That's fair. I would think that, over time, your priorities would naturally shift. Especially, I guess, as a startup founder.
In the beginning, you don't know how useful the model's going to be. You don't know if it's really going to see the light of day, even. And then over time, you really want to start to nail things down. You worry more about the downside risk.

Shreya:
Then you have to account for this infrastructure. Or transition in your organization, from Notebooks to whatever, if you want to deprecate them.
We interviewed one engineer who...they had this whole...their quarterly goals were to get evaluation of models out of Notebooks and put them in this standard system. Didn't matter what CI/CD tool or whatever, but the whole point was just get this in a standardized system, so that people would stop running Notebooks as a way to show that...and everyone had a different fork of the notebook.
I don't know, I feel like stories that just make me like, "Oh my God, no one is working on ML." No one is working on their direct company objective, because they're fighting their infrastructure battles and dealing with all the tech debt that they introduced from having the Notebooks.
What is the trade off? I don't know.

Lukas:
Were there other stories like that, or themes like that, where there's a consistent regret of something that people did in the beginning, that they now can't get rid of when things are in production?

Shreya:
The people who we interviewed that were more senior in their roles — or had been around for longer — just accepted this. It's like, "Oh yeah, organizational turnover is a thing. Tech debt is a thing. Our goal is not to remove it completely, but how do we keep shipping new things, keep old things up and running in the face of all of the tech debt?"
I think that's a more interesting question to me. There are a lot of one-off stories. I can't think of any off the top of my head that were specific to Jupyter Notebooks.
I guess there was one other anecdote, where somebody spent 3 to 6 months trying to reproduce some Jupyter Notebooks, just to make a point that they shouldn't use Jupyter Notebooks within their organization.
And then their organization had this push to — this was more of a smaller company — to get rid of Notebooks, or Notebook usage. Again, it's just so polarizing.

Lukas:
That's a little funny.
My honest experience with Jupyter Notebooks is I think they're kind of delightful, but I didn't...I predated Jupyter Notebooks, so I was doing most of my hands-on research before they existed, so I'm just a little more comfortable in the command line.
I always feel like a little ashamed that I'm not sticking with the new trends, but it sounds like there may be a backlash coming to these Notebooks.

Shreya:
I think it's also different. Different people are different. I'm the type of person where somebody hands me a Jupyter Notebook or something, "Here are some results," and I will be like, "Show me how the results got here." Because I'll be paranoid at every step of the way.
We talked about this in the paper. This paranoia, this sense of paranoia we all get. The same thing is...at least, the same thing is true for me when it comes to SQL queries. If you give me a SQL query, I want to know everything that's in your...I want to re-execute that SQL query so that I get the same result.
Same thing with spreadsheets. Give me the spreadsheets, don't take the screenshot of the spreadsheet and save it to me.
That's totally personal. I think people are different in their philosophies of how they do this. Which probably affects stuff.


Shreya's thoughts on ML tooling
Lukas:
Interesting.
What is your takeaway on the whole space of ML tooling? Obviously, I run an MLOps tools company, but please, you won't offend me with your answer here. I'm really curious.
Did you feel like people were using tools or were they rolling their own tools? Did you feel like they should...there's gaps and missing tools? Were you inspired to start a company in the space from the feedback that you got? I think it would be hard for me to contain myself, but I'm curious what your raw take is.

Shreya:
There's a lot of companies that could be started from that paper, but anyways...
I thought that the three Vs thing made tools — or at least the viability of ML tools — make a lot more sense. Like experiment tracking. Weights & Biases is a great example. It really 10Xs the velocity experience within experimentation, truly 10Xs it.
No longer do I have to go copy-paste my results into a spreadsheet and back and forth between training script and spreadsheet. It's just nice. Great velocity experience.
I think most tools that I've seen in this space don't really 10X in any of these dimensions.

Lukas:
What are the dimensions, for someone who hasn't read the paper?

Shreya:
Oh, velocity, validating early, and then versioning.
Versioning is an interesting...I think there's a lot of people trying to work on reproducibility and related — I have thoughts on reproducibility — problems, but it really needs to be a 10X experience in comparison to what people used to do with versioning, or with one of the variables.
I think that that's really hard to do in the ML tooling space. People are really trying to find that. People are, at least in my experience, simply trying to throw software engineering principles at ML workflows, and hope they land.
If it doesn't really push one of these variables, then it's unclear that, to me, it's a successful tool.
ML monitoring is also a really interesting space, because people do care about the concept of validating. I want to validate that my predictions are good before somebody complaints.
But it's really unsolved. How do we do this precisely? How do we not give people alert fatigue? I think people will go to a lot of extents to...the friction of integrating an observability or monitoring tool can be pretty high if you get results, but people are not getting results.

Lukas:
What are your thoughts on reproducibility?

Shreya:
There's an interesting paper... Gosh, I don't remember off the top of my head — this is bad, I should know — but they pose that, "Hey, exact reproducibility is often just not achievable in a lot of ML settings."
Just because, when you're a data scientist at a company and you're launching the job, yeah, sure you can control your random seed, but you can't control the infrastructure or the GPU provisioned to you, the underlying data that you called from.
What matters is getting some percentage-wise...if you're trying to reproduce a model, I want to get the same accuracy or a similar accuracy. I cannot rely on getting the same model parameters.
This notion quite...it's a little bit orthogonal to all of the provenance and instrumentation of ML workflows to get exact reproducibility. I'm not sure how feasible that is in a Kubernetes environment, for example, or larger-scale infrastructure.

Lukas:
To summarize your position, is it that reproducibility is impossible?

Shreya:
I think for reproducibility tools, we need to rethink what it means to get reproducibility.
Tracing, for example. Tracing a data scientist's workflow, saving the exact artifacts. Is that what matters? What is it that truly matters with reproducibility?
If I have the artifact but I can't reproduce that artifact, or if I logged artifacts at every step of the way but I can't reproduce them, does that help me?
I feel like these are questions that I don't have the answer to, off the top of my head.

Lukas:
I can't help but weigh in on my own thoughts here, because people ask me about this a lot.
I totally agree that reproducibility is much less of a binary switch then people realize. There's lots of things you can do that are increasingly annoying, to make things more reproducible. And I think there's a real cost, so you shouldn't necessarily do everything possible, but I do think most people would stand to gain from going further along that reproducibility tradeoff curve than they're doing today.
I always try to explain that to customers actually, of like, "Hey, we try to make it easy to save a lot of stuff, so that you have..."
Because most people's starting place — at least in my experience — is zero reproducibility. I'm talking about a model they made six months ago, they couldn't even tell you the state of the code when the model trained. Forget about the data that went into it.
I think every step towards reproducibility is going to make your team function better. It's going to help you with governance. There's so many reasons you actually would want to do it, but I think it is incredibly expensive to get perfect reproducibility, like you're saying.

Shreya:
Yeah, I like your definition of pushing further along the reproducibility axis. Then the question becomes, "Okay, what are the markers on this axis?"
I don't have an answer to this. I'm curious.

Lukas:
Well, if that's your next paper, I'll definitely...you can come back and tell us about it.

Shreya:
Not my next paper.


ML tooling layers, tech stacks, and workflows
Lukas:
You had another interesting...I love all the different frameworks that you're introducing here. I feel like you're really good at summarizing stuff and putting them into simple, CEO-style frameworks. You also had this notion of layers that tooling lives at. Could you maybe talk a little bit about that?

Shreya:
Yeah, this terminology caused a lot of controversy within the authors trying to come up with the names. I don't think anyone loves the four layer names that we have made. I don't know if they're the best.
We think about the stack of tools that an ML engineer interacts with, in frequency of "most frequency to least frequency", top to bottom.
At the top is this run layer. Then we think about a pipeline layer. Pipelines are made up of multiple components. Feature engineering, feature generation training, train/test/split, whatever components you want to have. And then at the bottom, underlying, is all this infrastructure that people use. Their compute, what is the workflow built on top of?
We notice or observe that when people want to make changes to their workflow, it's easiest to do in the run layer. It is much harder to kick something out of the infrastructure layer and replace that.
It happens in certain companies, but it's a big, organizational effort to do it. They all have many meetings. It's true, it's true.

Lukas:
What would be an example of a change someone might make at that layer?

Shreya:
Which one, the infrastructure layer?

Lukas:
The infrastructure layer, yeah.

Shreya:
I think one example is moving from GPU clusters on-prem to cloud GPU. That's one big one. Another one's introducing an orchestrator for these servers, like Kubernetes.
At least, these are things that I personally experienced, also at my previous company that was at. And even the pipeline layer is super annoying to make changes to. If you have Airflow, Kubeflow as your orchestrator, it is such a pain to migrate that.
Every planning meeting will be like, "And should we migrate?"
"Yeah, we know we need to migrate."
"Oh, but it's going to be so much work."
"Yeah, I know."
Stuff like that where it's...if I'm a tool builder, I really don't want to get into that space, because I'll have to sell so hard to people, to switch a tool at that layer.
In that sense, one thing we found is the open source tools that could be integrated at the run layer...Weights & Biases is actually a great example of this. Where it's like, one engineer can simply integrate that into their pipeline, and it will be useful for multiple runs of that pipeline. They're not replacing the pipeline layer tool.
We found that those were the tools that the interviewees were willing to adopt the most. But I feel like we could have done a lot more in running a survey, a quantitative survey or something, on this.
Maybe that's somebody's future work, whoever's interested in that. I'm hesitant to prescribe this as the end all, be all.

Lukas:
Prescribe the layers, or prescribe specific-

Shreya:
Oh yeah, the layers. And the idea of, "If you're trying to build an MLOps tool, don't try to replace TensorFlow or PyTorch."
Those people have their moat. People are not going to rewrite all of their deep learning models in your framework, maybe, unless you build-

Lukas:
What if it's JAX? Maybe they'll do it.

Shreya:
What if it's JAX? I don't want to get into that again. I don't want to get into these debates.
But it feels like one layer is easier than the other.

Lukas:
I really appreciate your open-mindedness about workflows and setups and I totally share it, but here we are in October 2022, and somebody listening to this podcast, they probably...I think what a lot of the people listening to it are looking for, is actually some help in navigating.
There's just so many options for tech stacks. SageMaker is not the same as Vertex, it's not the same as Azure ML.

Shreya:
Totally.

Lukas:
Where would you start?
Let's put on an example of a startup CEO, just getting product market fit, doesn't have a lot of resources, but ML is important to them. Where would you recommend him or her to begin looking at a stack? Or how would they think about that?

Shreya:
Great. I will say a stack that is tried and true...it may not be the best stack, but I would recommend getting a AWS account or something, having some EC2 cluster set up.
If you're working with large amounts of data...I have my qualms about Spark, but Spark is useful and people know how to use Spark as a query engine on large amounts of data. I would also-

Lukas:
-okay, okay, what are your qualms about Spark in a nutshell? Then we can continue.

Shreya:
I'm sitting in the lab where Spark was invented.
I don't like the idea. I think I subscribe to the database community of MapReduce as a philosophy of processing large amounts of data is not great, because it forces the application developer to reason about record-level problems.
If one record is corrupted, how do I handle it? It also forces the application developer to reason about consistency. If I'm controlling the parallelization, if I'm programming a Spark job, or MapReduce job, or something. I shouldn't have to do that if I'm a data scientist. I shouldn't be controlling these kinds of variables.
This is what DBMSs are really great for, they abstract away these parallelism internals. They abstract away ACID, how people achieve ACID. The DBMS is doing that.
In that sense, I'm not a really big fan of this MapReduce-style of work. It's also kind of inefficient to have a SQL layer on top of a MapReduce layer, on top of whatever the storage is. But that's a separate thing aside, that's not a really user experience thing.
As an aside, I think it's interesting the whole DuckDB explosion that we see going on, of bringing these kinds of large-scale data queries back to the DBMS. I'm curious where that's going to go.

Lukas:
Interesting.
All right, sorry, I totally derailed you, but you're saying AWS, EC2, start there...

Shreya:
Go get an EMR cluster for Spark and have some way for data scientists to interface with these machines.
Kubernetes...this might be a lot, but some way for them to access the machines that you have in your computing cluster. That's one thing.
I think another big thing is, once you get to production-level stuff, where if you have data pipelines at your company, you need to have some sort of workflow scheduler. Something to define a DAG and then execute those DAGs.
Airflow is really tried and true. I know a ton of people hate it, but it will work. It is also known to work in cloud-based settings, and they also have a nice Python DSL to be able to define DAGs. They have a nice UI to trigger the DAG. They have a nice UI to backfill the DAG. I would say that's good enough.
And then on top of that, I think people...hire a good data science lead, ML engineer to do the ML stuff.

Lukas:
Do you have any advice on hiring a first ML engineer or data scientist?

Shreya:
I wish. I almost want to say don't hire somebody right out of college, but I was hired right out of college, so I shouldn't say that.
But the problem with that was I didn't know anything. Here I was writing deep learning models in Jupyter Notebooks, saving them to S3, and then telling other people to read them.
No, that's a terrible workflow. A terrible workflow, if you want multiple people to collaborate on the same thing and share learnings effectively and also scale.
I think people who have data engineering experience tend to at least think about the right...not just terminology, but concepts.
SLAs are a good example of...ML people should also be thinking about SLAs. What is a minimum accuracy that my product should have before somebody complains about the predictions? Stuff like that.
How do I schedule things on a recurring basis? A lot ML pipelines can be casted as data pipelines, so I would hire somebody who has data engineering experience for sure. Ideally, hopefully someone who has trained a model, but I honestly think that's less relevant than having the data engineering experience.
I feel like I've talked to so many people who have ML experience but then don't have any software engineering or data engineering experience, and that's really hard to convert when you're starting a company.


Provenance and evaluating different solutions
Lukas:
Makes sense.
Well, we always end with two questions. I want to make sure we get them in. One is, what is a underappreciated topic in machine learning, broadly?

Shreya:
Machine learning...

Lukas:
If you were to go back into machine learning and could investigate something, where would you be wanting to look more?

Shreya:
That is not a data management problem. This is an exercise for myself.
I think the idea of interpretability, but I think of it as provenance. The influence functions paper is interesting. If I have an image and I have a prediction of this image, what are the training examples that most likely helped the model get to this image?
Techniques to do this are computationally expensive, or are limited to a single point in the training data, or require a full pass through the training set for every...I think there's a lot of work that can be done there on interpretability.
Not of the model, but explaining how a prediction got to where it is, based on the data that a model was trained on.

Lukas:
Interesting. Do you remember the name of that paper? I'd love to put it in the show notes.

Shreya:
"Understanding Black Box Predictions Via Influence Functions".

Lukas:
Nice.
And then I guess the final question — which you are incredibly qualified to answer, I think — is, when you look at the life cycle from research paper to running successfully in production, where do you see the biggest bottleneck, or the most surprising bottleneck?

Shreya:
Evaluating if this research — or this new idea — actually provides a worthwhile gain over another solution.
Is there something off the shelf? Is there something baseline that can get something very similar, or get a performance that's very similar, but not have to go through this headache of understanding the new thing and implementing this headache? I don't even think we have frameworks to think about this.

Lukas:
You're saying it's painful to try all the different things and see if they actually work?

Shreya:
Yeah. Do we even need to try all the different things and see if they work?
If I'm a practitioner at a company, when do I actually pay attention to some ML research development? When do I actually integrate it into my system? I don't think that people have a framework for thinking about this. At least I haven't heard of a big one.


Outro
Lukas:
All right, well thank you so much for your time. That was super fun. I really appreciate it.

Shreya:
Yeah, thanks for having me.

Lukas:
If you're enjoying these interviews and you want to learn more, please click on the link to the show notes in the description where you can find links to all the papers that are mentioned, supplemental material and a transcription that we work really hard to produce. So, check it out.

