---
title: "Passing the OSCP Exam: Trying Smarter"
parent: OSCP
grand_parent: Certifications
nav_order: 6
---

> The definition of insanity is doing the same thing over and over again, but expecting different results.
  
> <cite>Albert Einstein</cite>

If, like me, you have no hacking experience and no computer science background you have probably spent time in the Penetration Testing With Kali Linux (PWK) labs proving Einstein's theory of insanity. Presumably, you have searched online as to hints and tips about passing the OSCP. And there are no clear guides as to how to pass the exam with the author's *rightly* avoiding spoilers. You've probably also come across the tiresome phrase 'try harder'. Yeah, well that's a given, I'm guessing very few people signed up for Penetration Testing with Kali Linux without conducting some preliminary reseach indicating that the course and OSCP exam would be tough. My background is not computer science and I came at this from the more noob-end of the distribution of OSCP candidates. I have a PhD in Neuroscience, I feel as if I have the ability to learn most things, I believe its all about putting in the time. But, there's a lot of things I want to spend my time on, my time has to be spent efficiently. I did learn a few things on my OSCP journey that, if I'd have known at the start of the course, would have helped me greatly shorten my time to passing the OSCP and reduced the stress levels of doing the coursework/exam. We're all here doing the OSCP because we're prepared to 'try hard' and 'harder'. But let's heed Einstein's advice and try not to scratch around running endless dirbusters and nmap scripts trying to find the answer. Let's 'try smarter'. If I could do it all again I believe I could have been smarter about where I spent my time. I know realise that the PWK learning environment and the OSCP exam are not necessarily complementary. The PWK labs are a poor preparation for the OSCP exam. Maybe everyone else knows this but I didn't. I paid to learn in the PWK labs but the experience in there was very tough for a beginner. For a noob, I think it's much more efficient timewise to do very little time in the PWK labs, switch that time out for guided learning on HackTheBox, and use PWK labs primarily for the Buffer Overflow training prior to exam time. You have to buy PWK learning materials and lab time to take an OSCP exam attempt. Thats the way it is. But, thinking about it as PWK lab-time then OSCP exam isn't necessarly the way you should think about it. I beleive it's more time-efficient to do HackTheBox then OSCP. Let me explain the steps to enlightenment.

### 1. Dont buy the PWK course straightaway.
I paid for 90 days up front and wasted most of that time confused. In total it took me 5 months (I did 90 days PWK then 45-ish days on HackTheBox). In hindsight, I bet the exam was passable (for me) with the 30 day PWK-purchase after 60 days of HackTheBox. You may be different, you may be better, no problem. But my point here is to explain a way that may help some people shorten there learning period by cutting out the amount of time your in the PWK labs bewildered and lost. So, why does 60 days HackTheBox plus 30 days of PWK beat a pure 90 days of PWK? It's all about the learning process itself. In HackTheBox labs you learn. You have a great study guide for each individual box. In the PWK labs you have some brief introductions to the tools you can use then your left to muddle through. I did it the wrong way around. I bought the PWK time and expected that time to be an ideal learning environment. It isn't. With one exception (Buffer Overflow, which I will address later). 
When you buy the PWK course you get a pdf and some video content and access to the PWK labs. I had barely used nmap just once or twice on my home network. All the course material was new to me and I had no idea which information was important or not. The course materials are basic introductions to various tools/techniques you can use for penetration testing. After trying to get my head around the dry pdf material I started looking around the lab machines. I wasted so much time trying nmap and various other basic tools like dirbuster. Both these tools are critical for pentesting and passing the OSCP but I just felt like such a chancer when I was using them as I really didn't know how to exploit any findings that I did get from these tools. I was getting annoyed with how stupid I felt. I really needed a higher level overview of what it is to go from from nothing to a rooted box. Then I found HackTheBox. And Ippsec.

### 2. Get a paid HackTheBox account. 
HackTheBox has two tiers. Free and paid (I think about 15 dollars per month). The free tier gives you access to 20 machines. Just think of the HackTheBox free tier as the same as the PWK labs but with less machines. There's no real point in getting the free account. What I needed here was some handholding. What I needed was someone to show me how to hack a machine from start to finish. Then another machine, and another, and so on. Ippsec is that person. The paid tier of HackTheBox gives you access to what are known as `retired machines`. Those retired machines have 'walkthroughs' that you can watch either on the HackTheBox website itself or in YouTube (or pdf). The explanations for why each step is carried out are both clear and detailed. As you start to root more and more boxes following Ippsec's walkthroughs then it becomes very clear and obvious that he utilizes a relatively repetive and straight forward pattern to attack a box. Each machine on HackTheBox is also slightly different, so, although you will reuse many methods and tools, each new box you walkthrough you will learn something new. 
You can just watch the Ippsec HackTheBox videos on Youtube without getting a HackTheBox account. But for the cheapness of a paid account I'd just pull your wallet out, spend the money, and actually hack the boxes yourself (using a Kali VM which you can download from Offensive Security). In addition, you need to make notes on your work. Extensive, searchable notes that you can jump into during the exam as reference material. Furthermore, your note taking process in HackTheBox, and doing the PWK labs, will be the same process you use during the Exam itself as you may jump around from machine to machine and you need to know what you've already done (what scans/vulnerabilities you've already found). 
A Note on note-taking.
CherryTree is preinstalled in the Kali VM from Offensive Security. Its simple and you'll pick it up in no time. It's also searchable which is ideal. Here is an snapshot of my CherryTree notes from my HackTheBox work.

![image](/assets/images/htb.png "Some of the nodes from my HackTheBox activity")

Yes, thats also a `PWK` node at the top for the machines I'd worked on during PWK lab time. Each node in the HTB node is a machine that I walked through with Ippsec's guidance.

Finally, it must be noted, we're not just trying to rack up the numbers on how many boxes we rooted. Ippsec's videos are 20-80 minutes on average. In an 8 hour day you can blow though 10-20 of these boxes taking the easiest path and stopping halfway through the video once the box is rooted. And yay, you'll have 10-20 roots in a day. But,sometimes each box has several paths to root and those other paths are described later in the video. You don't know which path will come up in your exam. The first, the second, the third, so watch the whole video. Root the machine using all ways described in the video. What we are trying to do is broaden and deepen our knowledge not just 'get root'.

In summary, the OSCP exam doesn't care if you rooted 100 boxes in HackTheBox if you didn't retain any knowledge from it. 

The goals of using HackTheBox and the accompanying Ippsec videos are:
1. Understand the techniques used for each root (this takes time)
2. Make extensive notes on each root (this also takes time)
3. Use `1` and `2` in the OSCP exam.

### 3. Once you've hacked around 40-50 boxes on HackTheBox buy the 30 days PWK course.
You can give the pdf material a once over just for comforts sake. But to be honest it's not that useful. Remember the exception I mentioned earlier... The exception is the Buffer Overflow information. The most important box to root here in the PWK labs is the Buffer Overflow machine. Read the relevant sections in the pdf and watch the videos. Do the Buffer Overflow. Do it again. Do it **again**. Make a CherryTree note of how you did it. Look into the tools you used to develop the Buffer Overflow. These tools can be studied, they have more options and usefulness than the basic usage taught in the course materials. 

Why is this machine so important? 
1. This machine **will** be in your exam
2. It is a hefty 25 points in your exam. You only need another 45 points after you nailed this one.
3. You can learn enough about Buffer Overflow from zero to OSCP-exam-passing ability in a single week. That's one third of your exam points nailed in a week of study.
4. In the exam, these 25 points can be obtained in less than an hour. Leaving 23 hours to get the other 45 points.

Don't do the coursework. I put a lot of time doing the coursework and when I look back, yeah, I guess it was mildly useful, but, it was **not** as effective as doing HackTheBox machines. I learned more per hour of HackTheBox than I did per hour of coursework. Also, you're a bit in the dark as to how well written the coursework has to be. It appears you need to get all the questions correct for the measley 5 point. For the time you need to put into this effort and the uncertainty that you may miss the odd question (costing you the 5 points), I'd just ditch the coursework entirely.

You do have some of your 30 days left (after doing the Buffer Overflow) to play in the PWK labs. This will be similar to the actual exam environment so go ahead and try your HackTheBox skills in the labs. Its also time to schedule your first exam attempt. We will try and pass first time. But it may be a good strategy for you go into the exam chilled out and to use it as a learning experience for your second attempt. Once you've done the exam once, when you sit back and think about the points on offer for each box you can develop some strategies for attacking them second time around.

### 4. Take the exam early. Most people fail (several times)
The exams are cheap. They are also an intense period of learning (1. How to hack machines and 2. what your second exam attempt will contain).

Have your CherryTree notes ready. 
You CherryTree notes should have:
1. HackTheBox node stuffed with walkthrough notes on each machine. 
2. A PWK node with similar. The PWK node should have extensive notes on Buffer Overflow.
3. Brief summary on each tool or technology you expect to see. Especially with ready-made commands for tools like nmap, dirbuster, gobuster.

![image](/assets/images/cherry_summary.png "OSCP exam notes")

If you fail (likely). You will have gained knowledge on:
1. Oh yeah, the buffer overflow machine is in the exam, it is easy, and its 25 points in the bag in under an hour.
2. Learn the point-values on offer for the other machines.
3. If you bag the other easy machine how many point does that get you? How many more machines do you need? So the answer is obvious as to which two machines to spend the majority of your remaining time on.
4. Work out what the OSCP guys are thinking regards to Metasploit usage in the exam. You can't use it on the Buffer Overflow. You **don't** wan't to burn its usage on the low value machine. So... that kind of narrows its usage (but thats a good thing as it also narrows your thinking). You can see if Metaploit has a module for the exploits you discover in the exam without using the check function which is banned.

### 5. Take the exam again. 
A note on exam times. This may be very subjective. For exam attempt 1 and 2 I started at 10am and 6am respectively, coming off a normal sleep pattern (7 hours a night). In hindsight, for me, early exam starts were **another** terrible idea. During both early-start exam attempts I grabbed all low-hanging fruits and used most of my knowledge and skills in the first 6 or so hours. Then you try things over and over again and start banging your head against a light-bulb like a moth. Then it gets to night time... It's in those final 6 or so hours that you need to identify where you've missed the obvious clue for the box(es) your stuck on. You'll have scanned everything, dirbusted the hell out of every directory and you'll be stuck. Stuck and tired. Then you start to get pissed off at sunrise. Stuck, tired and pissed off as the sun comes up. For me, and this is the subjective part, I cannot work effectively 24 hours straight. So, on my final and succesful exam attempt. I had a start time of 6pm. I planned to stop around midnight and sleep for at least 6 hours. This worked **perfectly**. After 6 hours I had the Buffer Overflow machine, the low value machine and was well into 2 of the other machines. Buuuut, I was due a break. I'd taken all the low hanging fruit. I'd got some huge pointers as to where the initial route into both the boxes I was interested in. I felt good but I knew the longer I delayed going to sleep the more my performance would drop off. Then I'd start worrying that I didn't have time to go asleep if I wasn't making sufficient progress. If I didn't go to sleep then that would make the end of the exam (6pm tomorrow) a time 36 hours after I'd woken up (6am of the current day). If I thought it was hard to work 24 hours straight then no doubt its harder to do after already being awake 12 hours. So, I left my office (where I was doing the exam) and drove home. Even the simple act of leaving my desk helped. The brain gets stuck in these repetitive routines. Taking a break helps get out of these routines. On the drive home, away from my desk I worked out how to get into one of the two boxes I needed. If I could implement my idea and root that box it meant that I was free to use Metaploit on the other one. The next day, after a suprisingly good sleep in the middle of an exam, I arrived at work and immediately got a foothold in box that I'd solved on the drive home. I rooted relatively quickly. I then swicthed to the other box and Metasploited it in a few minutes. That left me about 8 hours to escalate privileges to root on the Metasploited box. I was so relieved I took my foot off the gas a bit and it took me several hours. Then I rooted the box with hours to spare. With the hours spare and the sleep in the middle I maybe only worked for 12 hours.

My first exam attempt was off the back of 90 days PWK.
My second attempt I'd scheduled shortly after the first. As I'd run out of PWK time I'd just discovered HackTheBox and Ippsec. I knew I'd hit a gold mine of useful material. I should have just cancelled the second exam attempt.
My third attempt was after a month or so of HackTheBox. 
The attitude was so different for each exam. For the first two attempts I was extrememly negative. i'd put chances at 10%. But on the third attempt I was bristling with confidence. 

### Passing OSCP in a nutshell:
1. HackTheBox & Ippsec
2. Buffer Overflow
3. A relative disregard for the PWK material and labs (not including Buffer Overflow).
4. CherryTree Notes on HackTheBox and BufferOverflow
5. A later exam start with some planned sleep.

The OSCP logo of the shadowy suited guy in the doorway that you get on your OSCP card is so lame. 
