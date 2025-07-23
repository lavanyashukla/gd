Anthony Goldbloom — How to Win Kaggle Competitions
and which jobs we should be worried about losing to AI in the next few decades.

Topics Covered
0:00 Sneak Peek
0:20 Introduction
0:45 methods used in Kaggle competitions vs mainstream academia
2:30 Feature engineering
3:55 Kaggle Competitions now vs 10 years ago
8:35 Data augmentation strategies
10:06 Overfitting in Kaggle Competitions
12:53 How to not overfit
14:11 Kaggle competitions vs the real world
18:15 Getting into ML through Kaggle
22:03 Kaggle datasets and kernelss
25:48 Favorite under-appreciated kernel or dataset
28:27 Python & R
32:03 Frameworks
35:15 2016 Ted talk through the lens of 2020
37:54 Reinforcement Learning
38:43 What’s the topic in ML that people don’t talk about enough?
42:02 Where are the biggest bottlenecks in deploying ML software?

Links Discussed
Watch his 2016 Ted Talk.

Transcript
Note: Transcriptions are provided by a third-party service, and may contain some inaccuracies. Please submit any corrections to angelica@wandb.com. Thank you!
Lukas: 
I remember you were talking about deep learning before I'd really heard about it. You were kinda the first person I knew that was really thinking about it, I think it's because you saw that people were winning Kaggle competitions with new methods that were less mainstream at the time. And I'm kind of wondering if on Kaggle, you're seeing people doing things that you don't think are on the academic mainstream or if you're seeing things that point to what you think could be mainstream production in the next few years. 


Anthony:
 It's a good question. I mean, to be honest, the most glaring thing that we see on Kaggle that is not fashionable in academia is that we're still seeing gradient boosting machines do very well on a lot of structured data problems. And there's not a lot of research attention on things like gradient boosting machines now. It begs the question like, have we done everything we can there, or is it an area where there is still more that can be done but it's just not the trendy thing? It's hard to get papers published and so it's just not getting the attention. To be honest that's the that's the most glaring difference we see between what is doing well on Kaggle and what is fashionable in the academic literature. 


Lukas: 
Well, it's really interesting. 


Anthony: 
We are seeing some novel uses of things like BERT and WaveNet being used on forecasting problems. We've seen BERT do really well on chemical informatics type or sorry, problems that have to do with gene sequences and things like that. So we're seeing like use cases, perhaps unknown use cases, for some well-established technologies but I think just the lack of academic-focused on these gradient machine algorithms is probably the biggest glaring distinction that we see. 


Lukas: 
And so in a structured data competition where gradient boost wins, what are the details that the winners do to win those competitions? Is it still feature engineering or is there other stuff? 


Anthony: 
Exactly. And it's finding clever features that other people aren't finding. Perhaps that's it. That's the reason or maybe that's where you could have more academic focus like otherwise to there is no doubt in my mind there are things you could do to automate feature engineering to some extent, and maybe there are some things that companies like Data Robot and h2o are doing when they are baking these recipes. So as an example, you see a date or a time stamp, for instance. That is an incredibly rich field that can become like 70 things, right? Let's say you're doing traffic forecasting, a timestamp can be turned into; Is it rush hour? Is it not rush hour? Is it a weekend? Is it not weekend? Is it summer? Is it winter? Therefore, does it change the probability of rain on a given day or adverse with no snow on the road and things like that? There are definitely things that could be done to automate components or help with some of the heavy lifting and feature engineering. And so, that could be an area of focus or perhaps maybe it's not an academic area, but it's the kinds of things that h2o and Data Robot and companies like that can build into their products. 


Lukas: 
Well, that's so interesting. So if you roll back ten years or you took a competition at the start of Kaggle and then you take it out today, how much better do people do? Do they even do better? Do you think you could win? Could you take modern tools and win every competition at the start of Kaggle? I guess my question is, has the feature engineering really improved? 


Anthony: 
So the thing when Kaggle first got started, people used to use all sorts of things like support vector machines, self-organizing maps, really a large range of things. The first big development that we saw or the first big contribution I think Kaggle made is we made it very clear that Random Forest was the best algorithm for actually most problems at that time, and then, let's say about 2014, Tianqi Chen at the University of Washington released XGBoost. I think it was always thought that gradient boosting machines should be better, you know. It's a very smart approach to run someway decision trees. They should be better. They're very, very finicky before XGBoost. When Tianqi Chen launched XGBoost,  it really took over from Random Forest. I'd say, unlike the difference between deep neural networks on computer vision problems versus Random Forest, the XGBoost increase is not a huge increase, but it was enough. And so, to be honest, unstructured data problems, I think that's probably where most of the software driven improvements have come from. It's probably the case if you took a problem from the early days of Kaggle, that was one with Random Forest and you reran it today, I think you'd get a little bit of a better answer because of the XGBoost. I don't actually think the way people are doing feature engineering has really improved very much. However, I do think that you would get.. What we always say is that Kaggle competitions, typically, you know, the top teams all converge on about the same level of accuracy and the intuition there is there's only so much signal in a dataset, right? And so people compete to the point where they've extracted all the signal. So I believe in the early Kaggle competitions, people always found that the key features and they got all the signal out of the dataset. I think what might happen is it had happened a fair bit faster now. If you think of professional athletes, they do a lot of training, Kaggle's communities are over five million people now. The people at the top are.. It's just like gone from more of an amateur sport to more of a professional sport, right? And so I think the difference isn't that the results would be better, but the top performers now would get to those results faster interestingly is my guess. Definitely. We ran a challenge with Pete Warden who's now at Google. He was running a company called Jetback and I think it was to distinguish competition between cats versus dogs and I think we did that, if I remember correctly, we did that before deep neural networks and afterwards and obviously saw a fairly big lift. We ran a challenge with the Allen Institute for Artificial Intelligence on solving an eighth grade science quiz. This was before the BERT innovations. People were getting about 60% accuracy using information retrieval methods. Allen have now run BERT-wide solutions on it. They're getting about 90%. So you definitely see... The before Deep Learning and after Deep Learning, you see very large changes in results for sure. 


Lukas: 
And I would think that on some unstructured data like language models and things would really make a big difference, right? 


Anthony: 
Yeah. I mean so you definitely have structured data where you have fields that are text fields, et cetera, et cetera. And so maybe you use language models to create features that ultimately go into. I mean, that's a common strategy. We run multimodel competitions sometimes where you have images and someone will run a convolutional neural network in order to come out with features out of that image, that then gets fed into a gradient boosting machine classifier. So that definitely happened. And so just as it gets done. For images that might be part of a multimodel dataset, of course, it can happen as well when there are columns that are text or data sources for a challenge that is text. 


Lukas: 
Are there interesting data augmentation strategies that you see people using? I feel like often people talk about that as a major area of innovation, and so do you see that on Kaggle? 


Anthony: 
There's a couple of ways people win Kaggle competitions. In the world of structured data problems, it's clever feature engineering. It's very often that, let's say for natural language processing or for computer vision problems, it's clever data augmentation that wins competitions. And some of my favorite example is the Kaggle community is really creative. I remember I think it was with Quora, we did a challenge around detecting insincere questions. I think that was the challenge and the winning strategy there or the thing that the winners did that others didn't do is that would translate the question from English to some other language and then translate it back, because if you use Google Translate, it's not a symmetrical translation, right? And so it was like a clever way to augment that dataset. So there are the standard techniques, you know, rotating, et cetera, for images. But then there are clever, creative tricks like that translation lap. There have also been a bunch of, you know, one of the libraries that have really taken off on Kaggle, I think was written by a Kaggle master. It's called Implementations, which makes it much easier to do sophisticated data augmentation, particularly on... that's designed for images, so it's definitely an area of a lot of focus in our community. 


Lukas: 
That's really interesting. Do you think that with feature engineering and augmentation being so important and then also like compute resources increasing, has overfitting in the training process become more of a problem over time, have people come up with new ways to address that? Like, I would think that if I'm just spinning through millions of possible feature combinations, I would end up overfitting on the validation data, right? 


Anthony: 
Earlier I said there are two things required to win Kaggle competitions; tenacity and creativity. I actually think there are three; and that's being statistically wise. So one pattern we see all the time with people who are competing in their first Kaggle competition is they'll submit, they'll be top of the public leaderboard and then what we do is at the end of a competition, we rescore everybody's algorithms on a second test dataset that they've never seen before. And also, let's say you put in, you submitted 150 models, you have to select two that get rescored, right? And so a very, very, very common pattern is that somebody will be on top of the public leaderboard. We then rescore them on the second test dataset and then they've dropped like 90 places. And it turns out to be an amazing way to learn the lesson of overfitting because, you know, you're staying up till midnight on leaderboards, ten over midnight UTC (that's when we reveal who actually won). And so you're staying up till midnight hitting refresh, refresh, refresh, you know, am I in first, am I in first? And you look at the public leaderboard in the private leaderboard when we switch over, you're not in first. You're not in second. You're in eightieth position. That person who overfits in a situation like that, they never overfit again. And I'd say that if anything, that was a bigger problem, coming back to your question, has overfitting on the validation set become more prevalent? I would actually say it has become less prevalent because it has become well known that to do well on Kaggle, you really need to be careful of overfitting. But just one more, kind of, adjacent point I want to make here is you'd be surprised that the credentials of some of the people who have had that happen to them where they're coming first and then they drop to a 100th spot, it makes me wonder how many of the world's research papers are actually overfitted. You know, how many of the world's algorithms and production or overfitted if experienced good people who have a lot of models in production or a lot of research papers out in the world, when they come to Kaggle in a place where they cannot overfit and they still overfit. Yeah, it really does make me wonder, like what percentage of the world's algorithms are actually overfit?


Lukas: 
I mean, it sounds really tough, right? Because I imagine myself in a situation where I'm trying to be statistically rigorous. But I think when you're testing lots of features, you know, I feel like it's tough to be perfectly statistically rigorous in that process. Do you have a sense of best practices that you tell people or where do people learn that they don't overfit at all? 


Anthony: 
I think it's cross-validation. I think cross-validation works well. There are techniques and as a Google researcher who has had a kind of clever approach. If you have a very small dataset, it's difficult to cross-validate where you don't get told that your algorithm outperformed unless it outperformed by a statistically significant margin you see intuition. And so you either get no information or you outperform by a meaningful amount... 


Lukas:
 That actually sounds pretty good, although you might miss stuff, I suppose but yeah, that's an interesting idea. 


Anthony: 
Yeah. I mean, I think cross-validation is still the right approach if you have a large enough dataset and if you don't, you know, but this technique is at least the one I'm aware of that allows you to still prevent against overfitting. 


Lukas: 
Interesting. Also, one thing I really wanted to ask you is you know, I think there's almost like this trope in the ML circus is that's like, you know, the real world isn't a Kaggle competition. I'm sure people ask you about this all the time. But I was curious what you think about what the differences are like, do Kaggle grandmasters tend to do well in the real world? Like what parts of Kaggle translates to actual applications, what parts don't? 


Anthony:
 So I guess there are... Let's back machine learning into, or building a successful productionizing machine learning model, into three stages. Firstly, you've got to turn your business problem into a machine learning problem. The second is you've got to try to classify that it's robust, et cetera, et cetera, and that it really works. And then the third is you have to productionize that classifier. Kaggle is obviously phenomenal for number two. I really think if you do well on Kaggle, if you train through Kaggle, you become as good as anybody in the world on number two. And I just want to maybe extend that a little bit more. Wonderful story from a very elite Kaggler, who's a senior engineer and leads an autonomous driving unit. He started there as a very junior engineer, and he made a name for himself in a bunch of, you know, well-credentialed people on that team. PhDs from famous machine learning universities had been working on a problem for three months. He took it home over the weekend and got way further over the course of the weekend than they had gotten over a three month period. And that's because Kaggle challenges you to see lots of different datasets and you're working to a deadline. And so he was able to look at that problem. He had seen enough problems directionally similar, had a good intuition for what the right approach was going to be and so he was able to come up with a very, very, very good solution very quickly. He's now a very senior engineer on that team, and that's how he made his name. And so I think Kaggle is outstanding for number two. People say we're irrelevant for number one, which is turning a business problem into a machine learning problem. I actually don't agree with that. I think Kaggle trains that muscle obviously less directly than the actual training of models. But the way it trains that muscle is, you see, the business problem is described in the text of the challenge and then you see how that team set it up. And so you see lots and lots and lots of examples of how different teams have taken a business problem and set it up as a machine learning challenge. The area where I think Kaggle gets dinged and fairly so, is on number three - taking a prototype model and productionizing. This is the kind of thing that really you have to be inside a company that's productionizing models in order to get experience. But  I don't think today that people are missing out on a lot. The process of having a model that has been prototyped in a Jupiter Notebook and then productionized is an incredibly painful thing. It's not like they're wonderful. And by the way, I think this will change over the next few years, but I don't think that somebody trained on Kaggle is going to go into a company and think, "oh, there's this whole world of things that are sort of well-established practices that I don't know". I think number three is currently a mess and it's a painful thing in just about any company you go and work for. So I just don't think that you're missing out on too much. Yeah, it's going to be painful whether you've come up through engineering at Google or you come out through Kaggle. 




Lukas:
 So I'm going to channel some of our audience. I know just from the comments that we get and the questions and the selection, I think we have a lot of folks that are trying to break into Silicon Valley-type jobs and I think Kaggle is a good way to do that. Do you have any advice for someone that's trying to get into machine learning through Kaggle? Like, have you seen that work for people and how that process is done? 


Anthony:
 Absolutely. Kaggle is now, at this point, a pretty well-recognized credential and in my view, a faster, more accessible way to break in than you know, a Ph.D. from Stanford or the University of Toronto. 


Lukas: 
In your unbiased view [laughs]. 


Anthony:
 In my completely unbiased view. I mean, we see people.. anyone who's a grandmaster on Kaggle, and I think if you work at it, you can get a PhD in five years. If you really work at it, you can go from, you know, an engineer who's OK with math to a grandmaster in a year. And it doesn't cost you whatever student debt, et cetera. 


Lukas:
 But how do you actually do that? Like, is it just doing competitions or... 


Anthony:
 It's doing competitions. It's reading the forums. It's we have Kaggle Notebooks where you can start with other people's code. You focus, you ask a lot of questions in the forums and you can become a grandmaster across one of four dimensions. You can be a Competition Grandmaster, a Datasets Grandmaster, a Discussion Grandmaster or a Notebooks Grandmaster. In rank order, the most respected (probably by employers) is Competitions in my view and justifiably so. We prefer people who are either Notebooks or Discussion grandmasters, and the reason being is you have to be insightful enough that you're writing comments that people upvote or you're writing notebooks that people upvote and you have to write clear enough code or communicate clearly enough that you would also make for you know, the kind of thing you want on a team. I would pick one of those three categories and the kinds of places... Invidia has hired somewhere in the order of 20.. 10 to 20, I'm not sure the exact number of grandmasters over the last, let's say, six months. So they've been on a hiring tear for Kaggle grandmasters. Deep Mind has hired quite a few, h2o have a team of about 15 or so Kaggle grandmasters. So it's not a credential that every company goes for, but a meaningful amount of top AI companies have valued this credential. And then once you've got your first job, you're in right? You'll continue to get other good jobs. 


Lukas: 
I feel compelled to add that I also love to see Kaggle credentials on a resume in Weights and Biases' top ML company. But I'll say for me, I even appreciate, you know, we hire a lot of engineers back and front end and sometimes they'd be like, "hey, I did a couple of Kaggle competitions". And I think that just says so many good things about a prospective employee, I'd love to see it. So I just totally agree with you. I guess I'm maybe slightly less obviously biased, but I love Kaggle credentials and I love it when people share them on their resume. One thing I want to make sure I had time to get to, just because you've told me privately I think, that in some ways the maybe lesser known publicly Kaggle products have in some ways more traction than the competition product, right? Can you say what the other ones are and why you decided to build them and how they're doing? 




Anthony: 
Yeah, sure. So Kaggle's, between 2010 and 2015, we were an all machine learning competitions. We always thought that machine learning competitions are very powerful, but also not going to appeal to everybody. And as data science machine learning grows as a profession, we wanted to make sure that we were continuing to grow with it. The first thing we launched is Kaggle Notebooks, which is basically a hosted Jupiter Notebook. And really, it doesn't cost you anything. You get a CPU, a GPU or a TPU so you get as much CPU as you want and then you get 30 hours a week of either GPU and TPU. So you get quite a lot of free accelerators. 




Lukas: 
It's so great that you do that. It's awesome. 


Anthony: 
You know, we're part of Google. We would not have been able to do this as a standalone company. But the really nice thing here is you come to any notebook on Kaggle, you can hit the copy and edit button, we used to call it Fork, and you get somebody else's code running in an environment that will run it, right? So it's completely reproducible. We launched it initially inside competitions because we noticed people sharing their code in forum posts, either linking to a GitHub repo or attaching a Python script. We also noticed that those forum posts. People came to Kaggle to learn, those that should be the most valuable forum posts, they got dramatically less interest than forum posts where people shared ideas. So it's like the most valuable content was not really getting utilized and that's because, you know, you get someone's Python script, you have to get the same version of Python, the same version of... you're on the right side of Tensor 1.0, 2.0, like all these dependencies, really takes some number of hours to get somebody else's code to run and then you don't know if it's any good. And so if we could create an environment where it was much easier for people to share code and not have to worry about the environment behind it, and that was the insight behind Kaggle Notebooks. We have somewhere in the order of 800,000 users every month.. I'm on parental leave so my knowledge of the data might be a little out of date. It might be over a million people looking at other people's notebooks, which is just extraordinary. The other product we have, kind of like how people share videos on YouTube, we allow people to share datasets on Kaggle and where this grew out of is we noticed when we launched Kaggle Notebooks, they were initially only useful for people competing in competitions to share code alongside competitions. But we noticed people using Kaggle Notebooks to share more free-form Insights, and so it's like, oh, wouldn't it be great if we gave people datasets as well, that they could do more free form type work on? And so we launched this platform where anyone can share any dataset. And we have, at least last time I looked at the metrics which again was before parental leave, was over 400,000 people downloading Kaggle Datasets. So I think these are.., remember the word data science machine learning side it's still an emerging profession and to have those sorts of numbers on these products, it means that they're getting really meaningful traction. 


Lukas: 
Yeah, it's really cool. 


Anthony: 
And they're also a nice way. Like Kaggle competition is a tremendous commitment. If you want to get involved in Kaggle but don't have the time to put into a competition, these are ways to get involved in a lot of white way. 


Lukas: 
Do you have a favorite kernel or dataset that maybe doesn't get as much attention as it deserves? 


Anthony: 
There are lots. There are all sorts of things. Somebody uploaded a dataset taking x-rays, and you had to predict the age of the person based on their x-rays. It was called the Bone Age dataset, which I thought was kind of cool. 


Lukas: 
That is really cool. 


Anthony:  
Just like really random. Aww man, what else? We've got a lot of cool covid-19 datasets. One of the things that has been nice with the covid-19 datasets that have been shared is that, you know, you've got the John Hopkins University dataset, for instance, and everyone's looking at that. One thing that people have been doing on Kaggle which is really powerful, is they've been creating these very rich panels where they join the John Hopkins dataset to daily data from the nearest weather station. And so there's this debate about how does temperature and seasonality impact the transmission of covid-19? Well, somebody has just.. And I've seen some of these studies, like some study, will look at 100 cities in China and draw some conclusion about the rate of transmission and how temperature impacts. Well, people in Kaggle communities just hand-delivered all well over 4000 locations with the nearest weather station. And so those that those kinds of things are also, I think, really cool and really powerful.  




Lukas: 
That is so cool. And it's been out for four or five years, I guess. 


Anthony:
Kaggle Notebooks launched in 2015 and Datasets, that was about May. And by the way, Kaggle Notebooks really started as an edit box with a run button. We also launched very lightweight. We launched with R, not Python. 


Lukas: 
Oh, wow. That's a sign of the times. Wow. That is amazing. 


Anthony: 
The number one feature request was can you add Python? Although I should say some of the most beautiful Notebooks are written are still particularly for data analysis, data visualization. It does really well on Kaggle, beautiful content still created with that and then Datasets launched in August of 2016. 


Lukas: 
It's funny. I really want to ask, these are just the questions I selfishly want to ask, but I guess it's my show so I can do it. When you look at the tools people are using, I mean just as an example, do people use anything besides Python and R and do people actually like win competitions with R? I say this as a long time R user who switched to Python so I'm not against R but it does seem like almost everyone has switched at this point. 


Anthony: 
Yeah, I mean, when Kaggle first started, it was like Matlab, we even saw SaaS, we saw a whole lot of stuff and then it quickly became R and then Python's rise has just been sort of a fairly steady, it's just like steadily taking share. I'm not actually sure what the numbers are. Now, I know a couple of years ago it was two-thirds python, one-third R. I suspect it's probably closer to 90% Python, 10% R now. I'm actually not certain of that, though. I'm not aware really of R doing particularly well in Competitions. I think Python is hard to beat, like the support for neural networks, et cetera, et cetera, is, I think, a fair bit stronger in Python. And so I'd say the place for R has really shone in the community is beautiful beautiful Notebooks. You know new competition launches, somebody writes a Notebook. We have a user I have in mind when I think of, you know, I have a persona in mind, heads or tails is a Kaggler who writes beautiful R Notebooks, sort of helping anyone competing in the competition get their arms around what's in that dataset. So it still plays a nice role. I'd say that we've seen a bit... To the extent that people are using different types of technologies on Kaggle, we had a challenge fairly recently where h2o's driverless AI did really well. It was a forecasting challenge. We've had challenges in the past where Google's autoML has done well. I happen to be a huge believer in that category. You know so much of turning your own network is turning knobs, why shouldn't that be automated? Even so much of feature engineering, and we spoke about this earlier on, exploiting a date can probably be written into the software. So I'm a huge believer in the next big thing in terms of model training is probably more and more automation of the things that are relatively easier to automate. And then the other place that we've seen new technologies get adopted, as some of the things that are generating excitement in the community, we launched TPU Notebooks and certainly some class of problems where TPU is doing extremely well, particularly on the natural language processing models, which are very, very, very memory heavy. I think there's a lot of excitement and videos coming out with a new chip soon, which I think there's a lot of excitement around. So any advances in accelerators get people excited. 


Lukas: 
Is this faster training times or literally the models perform better? 


Anthony: 
So one of the reasons that faster training times matter is because we give people nine hours Kaggle Notebooks. So it's faster training times, but a lot of people are using our Kaggle Notebooks and so the fact that you can train a model faster, there also are some issues, I think that people have trained things like RoBERTa, which is a particularly memory intensive version of BERT and so the TPUs we make available have enough memory such that you know, it's the difference between being able to train a RoBERTa model or not. 


Lukas: 
What about frameworks? How do they break down? Is everyone using TensorFlow or what's ...? 


Anthony: 
No, I think PyTorch is really... We just see PyTorch is doing really well. Actually I don't know what the... TensorFlow 2.0 is obviously a big release. People love Keras. It's really Keras has dominated on Kaggle for a long time and now Pytorch is..., I'd say maybe Keras and Pytorch, at least last time I checked, was sort of roughly equivalent, the trajectory on PyTorch was very strong. I don't know that I have a good sense of the extent to which TensorFlow 2.0 has, you know, changed the PyTorch TensorFlow, you know, what that trajectory looks like yet, but certainly PyTorch's rise has been very, very, really incredible. 


Lukas: 
And what about the simpler layers on top of PyTorch like Lightning and Fast AI and Ignite, like do you see those? 


Anthony: 
Yeah. I mean Fast AI, definitely, we see I think fast AI. Quite a lot of people do that course and then Jeremy mentions Kaggle a fair bit in that course. And so I think that ends up being a decent feeder to Kaggle and so people coming out of that course bring fast AI, the other two not so much 


Lukas: 
Is there like.. Do grandmasters have a different sets of tools? Like do you see the more experienced people switching to stuff or...? 


Anthony: 
I think what they often have is not so much their own tools, but they very often have built, what's the way to put it, their own little framework so that when they see a computer vision problem, they're not starting from scratch, but they're starting with code that they know well, that they know how to optimize well. And by the way, the fact that so many grandmasters are creating their own little frameworks suggests that the PyTorches and the Tensorflows aren't, you know, there's something missing or maybe it's that people like to do things in their own way or maybe they're like slightly too low level for the kinds of things that people are doing in the Kaggle community. 


Lukas: 
So what are the common things that these frameworks do? 


Anthony:
 I think they're very often like all the pipeline steps, right? So you've got your new image dataset come in and the first thing you want to do is you want to do data augmentation and they have their preferred way of implementing data augmentation and then passing it on to the next. So I think it's really focused on creating a pipeline that starts with a new dataset and then ends in a Kaggle submission file. 


Lukas: 
Okay, I want to totally shift gears because there's a couple more questions I want to make sure I get to in this time. So this is actually a Lavanya suggestion for a question, and I love it. So I remember you giving a TED talk about the jobs that we'll lose to machines. I remember you telling me about it. I thought it was super smart and you had a way of thinking about the jobs that you should be worried about losing. So I was hoping you could describe that to this audience who maybe haven't seen the TED talk, but I also was wondering if your thinking has changed at all since you gave the talk, because that was in 2016 and now things have changed a bit.  


Anthony: 
Yeah. At the time maybe it was slightly not obvious to me. It reads now, it's like very obvious. The basic conclusion is jobs are at risk if you're doing the same thing again and again and again. Kaggle had done a path-breaking competition, taking images at the eye and diagnosing diabetic retinopathy and the results on that were just outstanding. And we've done a lot of other medical imaging problems. And you think about what... This is fairly hackneyed at this point, but a radiologist does the same thing again and again and again. Looking at an image, making a diagnosis of that image; or an ophthalmologist. Whereas if your job requires you to be creative and to be sort of doing different things on a daily basis, you're probably much safer. You know some of the professions, I think I mentioned in the talk, at least I had in the back of my mind that surprisingly haven't gone, you haven't seen much automation yet, is like auditing, getting basically legal contracts, like "do you really need a lawyer to look at yet another relatively boilerplate NDA?" "Do you really need an auditor to go over the majority of the company's accounts?" are probably fairly standard. So there's still a lot of work that in the four years since the talk and I'm not aware of a ton of work being done to automate. So it sort of points to perhaps opportunities or perhaps things that still haven't been done. But I think the conclusion still stands. You know, I was in 2016 fairly skeptical that we were going to make a lot of progress towards Artificial General Intelligence. I still.. I just don't see it. The current set of tools that we have, I think, are incredibly useful and they are very powerful and they allow us to do a lot of really cool things. I don't see a path from where we are, a smooth path that doesn't involve multiple step changes from where we are today to AGI. And the distinction between repetitive tasks and tasks that require more creativity and more moving around still to me is true as where jobs are aside from where they aren't. 


Lukas: 
Do you have any opinions on reinforcement learning? I feel like we've seen a lot of interesting stuff coming out that certainly feels like a different kind of intelligence to me. Have you looked at that?   


Anthony: 
Yeah, I guess with reinforcement learning, where Kaggle aims to be is somewhere between where the cutting edge of academia is and where the average Fortune 500 company is. So I guess we believe in reinforcement learning enough that we've started actually, I guess two or three weeks ago, we launched our second ever simulation competition. It was with two sigma where people are writing AI bots to beat each other in a game called Haywire. In January, we tested the concept with a game of KinectX and so we are now investing in reinforcement learning. You know I have heard of some cool, pragmatic applications as well covered, deep-mined, optimizing data Google data centers. I've heard about potential uses and search and ad targeting in stock market trading so I guess I'll start to get excited when there are more, Kaggle is excited enough that we're investing and that we're making reinforcement learning challenges available to our community. I'll be more excited than I am today when there's more pragmatic use cases that we can point to where it's really making a positive difference. 




Lukas: 
That makes sense. Alright. So we always end with two questions. The penultimate question here is what's the topic in machine learning that people don't talk about as much as they should? 


Anthony: 
I mean, one of the things I'm really energized about at the moment, just particularly with the success of Catalyst datasets platform, is I want to make it easier for people to find access and join external datasets to their own datasets. There are raw materials, right? So the easier it is for us to integrate them into our machine learning algorithms, the more powerful our work is going to be. And so that's one area. And then the second one is one I mentioned earlier; Algorithm boosting machines still to incredibly well in Kaggle challenges and it's just not an area of academic study at all. And it makes me wonder, is there more that could be done? Is this an area that's being overlooked? Is there more that could be done around gradient boosting machine-like technologies? Have we abandoned too fast?  


Lukas: 
It's funny, I worked a lot on gradient boosted trees back in the day. It's probably the algorithm that I spent the most time with and I remember feeling like they had trouble learning linear relationships like they're so good, you know, these step function things. But is it just gradient boosted trees or do we add more weak learners to their gradient boosting? 


Anthony: 
What we typically find with structured data problems is people who're trying to, with their text-u boost or LightGBM or some gradient boosting machines framework and if you look at it, that is what's doing 99.9% of the work and very often people will ensemble in other things just to get a bit more diversity. In most cases, I think that it really, sampling other things, helps take you from twentieth to first. But actually when a company looks to productionize a model that comes out of a Kaggle challenge, they will strip out all the other stuff because you just don't want the complexity. So I think gradient boosting machines is really, typically, enough on most structures. That plus clever feature engineering is enough on most structured data problems. 


Lukas: 
Definitely. I classify that as interesting. The final question is, when you look at, and this is maybe outside of Kaggle, but like at Google and all the companies that you've talked to, when you look at the path from inception to deployed machine learning software, where do you see the biggest bottlenecks? 


Anthony: 
I like this analogy. There's this company at the moment that's pretty hardcore web flow. And what they do is they help with the same between a designer and a front end engineer by making it much easier to get a design into HTML, CSS, JavaScript code. And I think that's probably an area, taking a prototype model written in Python, possibly in Jupiter Notebooks into a production system, you know, maybe the production system is in Java or something else is really nasty. You've seen a bunch of companies invest. Google obviously is invested internally, invested in a system called Michaelangelo. There's a lot of systems that have been built inside companies to try and solve that problem. But a bunch of startups now are trying to take those systems that have been built internally for the likes of Google, for the likes of Uber and to make them available to the wider world. I think that's definitely a problem that urgently needs to be solved. The same between data scientist and machine learning researcher and data engineer is a really [nilees] scene at the moment. 


Lukas: 
Well said. Awesome. Well, thanks a lot Anthony, that was actually fun. 


Anthony: 
Cool, thank you. Thanks for having me. 
