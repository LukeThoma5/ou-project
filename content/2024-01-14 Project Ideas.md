---
date: 2024-01-14
week: 2
time:
  - task: "[[Initial Ideas]]"
    time: 5 hours
    progress: 60
---
Date: Sunday, January 14, 2024
# Work Undertaken Summary
- Read Idea's guidance and forum guidance
- Come up with 2 project ideas
- Flesh out the ideas / initial brainstorm
- Clean up ideas and post to the forum for feedback
- Respond to feedback

# Problems encountered and how you overcame them
Not Applicable

# Time Spent
```dataview
TABLE WITHOUT ID
link(meta(entry.task.top-level-task).subpath) As "Top Level",
entry.task as "Second Level",
entry.time As "Time",
entry.progress as "Progress (%) this week est"
WHERE time != null
WHERE file = this.file
flatten time as entry
sort date desc
```

# Questions for Tutor
Not Applicable

# Next work planned
Decide on Project idea with tutor when allocated.

# Raw Notes

## Level 3 Modules

Systems penetration testing (TM359)
Data management and analysis (TM351)
Software engineering (TM354)

# Project Ideas
1. Reverse engineer specification with LLM
2. Create an app to find traumatic faces and remove from images.

# Is the idea suitable
[TM470-24B: Project preparation | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/forumng/discuss.php?d=4482497)

1. The project must be substantially within the computing and IT domain.
    Done
2. Projects should build on one or more of the computing and IT subjects you have studied (or are studying) in your level 3 modules, or where you already have knowledge and skills at an equivalent level in computing and IT, by building on and extending that knowledge and skills.
    LLM - Software and data management.
    app - software engineering
1. It applies learning from level 3 and techniques or analysis beyond those you have studied already in order to solve a problem that is either practical or has a strong practical context.
    yes
4. Projects must include undertaking practical work of some sort using computing/IT technology.
   yes 
5. Projects must demonstrate the ability to apply practical and analytical skills.
    yes
6. The project meets a real need in a wider context.
    yes
7. The approach to the project should demonstrate that you can learn independently, effectively manage your time, develop appropriate new skills and knowledge using your own initiative.
    LLM - Learn how to interact with and get positive results out of an LLM
	app - how to use webasm
1. The project should demonstrate the ability to plan and organise your time and your project work appropriately, and keep systematic records of plans, progress and outcomes right from the start, and maintain and update throughout the project.
    Both are a project with outputs that requires planning.
9. Where the project has a core focus on research or evaluation, substantially within the computing and IT domain, you need to produce a report that covers all aspects of the project development process as as well as clear evidence of the  outcome of your research or evaluation.





## Working Title Advise
_Working title_

The title should be short and clear. In many cases, it will be possible to develop a title that refers directly to the main practical _output_ of your project. One tip is to avoid describing the project exclusively in terms of the technology(ies) you will use (databases, Java, etc.). Instead, you should foreground the nature of the problem you are trying to solve (‘a customer–relationship management system for an internet music retailer’, ‘a community consultation forum for a parish council’ etc.). A good template that combines the two is: `A <something> for <something> in <some context>.

_Description and scope_

There are many ways to describe your project. One useful framework is to give short, one- or two-sentence answers to each of the following questions:

- What is the problem?
 - Why is it considered a problem?
 - What will be the benefits of solving it?
 - What might the solution look like?
 - What, specifically, will you deliver by way of end product?

You may need to adapt some of these to suit the nature of your topic, but everyone should have a clear and simple answer to the last question.

Be realistic about how much you can achieve in the project – most practical projects take much longer to complete than is initially estimated (ask any builder!). Here are some useful questions to help you scope your project:

- What am I going to analyse, design and then deliver as an end product?
 - How am I going to identify the (basic) requirements?
 - How will I implement the solution: iteration?, incrementation?, both of these?  some other strategy?)
 - How will I evaluate it?

Aim to have one-sentence answers to each of these.

And what about literature? Well, you will have materials from the related module(s) that you are drawing on. You may have your own favourite sources on technologies and techniques, be they textbooks, O’Reilly books, xxx for Dummies, etc. Additionally, you will need to think about academic literature. The best way to access this is via The Open University Library website. When you have a specific project title, you’ll be in a good position to search this collection. (See the materials on searching and reviewing literature and additional guidance on the Library website.)

The Project discussion forum has an area where you can submit an early draft of the above. In fact, it is a good idea to access this site at an early stage. The site doesn’t offer feedback to every submission, but it does respond to submissions where a more general point arises.

# Writeup
Approximately 3000 user stories.

## Luke Foreman TM359 TM351 TM354 (All Complete)

I have completed my 3 level 3 modules:
Systems penetration testing (TM359)
Data management and analysis (TM351)
Software engineering (TM354)

I have two project ideas, feedback on which is more viable would be greatly appreciated.

# Idea 1

Working Title: Reverse engineering a complete software specification from 7 years of User Stories.
## What is the problem?
For the last 7 years I have been working full time as a software engineer, primarily on a single very large project. This project has been developed in an incremental and agile manor, with approximately 3000 user stories generated and approximately 14 years of engineer development time.

The project is incredibly complex, and has evolved quite considerably since initial development. Occasionally with a flip-flop between what is and isn't allowed / the system needs to handle as requirements evolve.

As a result only 2 people know the entire history of the project and how everything interrelates. The goal of the project is to produce a single accurate specification for the project which can then be maintained going forward.

These people are now bottlenecks for discussions concerning future changes to the project and without a unified source of truth both the client and the developers can claim apposing attributes of the system to be true as they both were at one point in time.

## How will it be solved?

The OU project would involve exporting and massaging the User Stories into a format for consumption by the LLM.

Running the data through the LLM and evaluating its output on:
1) Accuracy - Number of errors - categorised e.g. Hallucinations vs outdated information
2) Conciseness - To be a useful specification it must not repeat information and must be legible to the reader
3) Completeness - To be useful for describing the system it must cover everything to a sufficient level of detail

The process will be repeated for different LLM models:
1) GPT-4 (OpenAI/Microsoft)
2) LLama 2 (Open Source/Meta)
3) Gemini Pro (Google)

And repeated for different styles of generation:
1) Train on complete dataset and then produce specification
2) Incrementally introduce User Stories to evolve specification over time.

### Module Relevance
Data management and analysis (TM351) - Manipulating the large dataset + issues around data serenity 
Software engineering (TM354) - The specification process, agile development, building of software to run the large language models against the dataset.

## Legal / Ethical considerations
I've been cleared to use the data set but would not be able to provide the complete dataset or final specification as it would include business IP. But I would be able to discuss challenges with the process and provide relevant excepts.

# Idea 2

Working Title: A face scrubbing web app for trauma victims
## What is the problem?
Having broken away from abusers, victims are faced with large chunks of their memories/photos being inaccessible due to it containing reminders of the abuser, specifically their face. Sorting through these photos is too great a task and so the victim loses memories of a good portion of their lives.

## How will it be solved?
The app that I would build would be a progressive web app (PWA) that runs entirely in the browser (no privacy concerns as it never leaves the user computer). The flow would be selecting a directory of photos on the computer, the webapp scans the images for faces and classifies the faces so that the same face appears once. The user selects any faces that they want removed and the webapp re-encodes all the images with the offending faces blocked out. Allowing the victim to safely revisit their precious memories.

The project would be a standard software development project with specification, diagrams, test cases etc.

The project would be built using PWA technologies (directory access / web workers) and WebAssembly (reuse existing face detection/classification libraries, reuse image encoding https://squoosh.app/)

Relevant module - Software engineering (TM354). Project planning / delivery of a software artefact


# Reponse
Hi Ju,

Firstly I want to apologise if my #2 idea came across as offensive. I should have been much clearer that I was referring to the Facebook/Google Photos "memories" feature where it brings up photos from your past in various categories. Like you x years ago, your trip to y etc.

The idea is very close to my heart as it was inspired by my partner who has been victim to some abusive partners before. Whenever they appear in the photos it sends them spiralling and causes them unnecessary grief. They don't want to delete the photos as they document their early adult years. While they possess the needed skills to edit the photos themselves, going through all the photos would be an incredibly painful exercise. So by letting a computer do all the heavy lifting it lets them reclaim their photos without inflicting unnecessary harm to themselves.

My partner loves the idea so I am going to do it for them. Whether its my OU project determines if it'll be a one off hacked together script or if its made into a more generally useful and privacy focused web app.

Regarding the skills needed to complete the work, while I've only briefly worked with WebAssembly before I am a professional software engineer with 7 years experience of full stack web app development so I should be able to complete the project.

Regarding idea 1, GPT-4 and other large language models will be used to create the specification. E.g. we have 3000 user stories detailing how the system should operate, some of which have been superseded. So the idea is to incrementally feed the LLM's the user stories / change requests so that it gradually builds up an idea of what the system is supposed to do. Having been on the project from the very beginning I'll be able to review the output of the LLM and grade it on the criteria to then compare techniques / language models. Which I hope would prove an interesting investigation. To clarify by "reverse engineering" I mean taking a stack of user stories and turning it into a specification, as opposed to the traditional waterfall approach of writing an all encompassing specification which then gets split into thousands of work items.

Thank you for your feedback :)

# Reasoning
I am prefering the LLM project because:

1) Requires learning a new domain / skill - more to write about
2) Requires academic reading
3) Requires more analysis, e.g. comparing results against each other.
4) Useful for work, social benefit there
5) Can be turned into a work knowledge share / talk
6) Has clear stakeholders