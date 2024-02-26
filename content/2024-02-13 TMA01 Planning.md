---
{"publish":true,"path":"2024-02-13 TMA01 Planning.md","permalink":"/2024-02-13-tma-01-planning/"}
---

Date: Tuesday, February 13, 2024
# Work Undertaken Summary
- Document Logbook choices
- Setup Logbook
- Setup Timesheet + reporting
- Setup Quartz (publish the notes)
- Fix DataView on publish
# Problems encountered and how you overcame them
Had to learn how DataView works. Especially the edges of the query language to enable queries around the complex object for the time property. Was able to get it to work using the examples provided by [Dataview (blacksmithgu.github.io)](https://blacksmithgu.github.io/obsidian-dataview/)
[seburbandev/obsidian-dataview-cheatsheet: This cheatsheet provides a handy reference guide for writing powerful queries using the dataview plugin in Obsidian. (github.com)](https://github.com/seburbandev/obsidian-dataview-cheatsheet)

Publishing straight using quartz has the problem that the dataview plugin isn't executed during publish. So what is published is the raw query rather than the results of the query. Which is not useful for sharing with my tutor.

Thankfully this week a new tool called quartz-syncer was released that allows the queries to be run and baked in prior to publishing.

# Time Spent
| Top Level                                    | Second Level                                                          | Time               | Progress (%) this week est |
| -------------------------------------------- | --------------------------------------------------------------------- | ------------------ | -------------------------- |
| [[TMA01\|TMA01]]                             | [[Tasks/TMA01/Log Book\|Log Book]]                                 | 6 hours            | 80                         |
| [[TMA01\|TMA01]]                             | [[Tasks/TMA01/Blog Setup\|Blog Setup]]                             | 3 hours            | 100                        |
| [[Recurring Tasks\|Recurring Tasks]]         | [[Tasks/Recurring Tasks/Tutorials\|Tutorials]]                     | 3 hours            | 20                         |
| [[Data Transformation\|Data Transformation]] | [[Tasks/Data Transformation/Retrieve Database\|Retrieve Database]] | 1 hour, 30 minutes | 100                        |


# Questions for Tutor
N/A

# Next work planned
TMA01

# Raw Notes
## Log book
Talk about using obsidian as my log, and how I've set things out. With dates in the file names (find what the name of that note taking method is) and explain the reasoning:

1) Local notes
2) markdown files - very portable.
3) Easy mix of media (code, notes, emails, )
4) spellcheck
5) free for academic use
6) Easy cross linking of notes / ideas
7) good search
8) easy share with tutor [Hosting (jzhao.xyz)](https://quartz.jzhao.xyz/hosting)

### Obsidian Setup
[My Obsidian Daily Note Template | Dann Berg: blog, newsletter, shop, and more](https://dannb.org/blog/2022/obsidian-daily-note-template/)
[How to Use YAML Front Matter in Obsidian (2024) - WunderTech](https://www.wundertech.net/yaml-front-matter-in-obsidian/)
[Dataview (blacksmithgu.github.io)](https://blacksmithgu.github.io/obsidian-dataview/)
[seburbandev/obsidian-dataview-cheatsheet: This cheatsheet provides a handy reference guide for writing powerful queries using the dataview plugin in Obsidian. (github.com)](https://github.com/seburbandev/obsidian-dataview-cheatsheet)


#choice Using DataView so that as much as possible is kept within the logbook. A singular source of truth. Makes it easier to match up time spent with the activities. Easier to communicate with tutor. Less context switching.

### Obsidian template
Template includes:
Date - For easy tracking
Time - To show time on the weekly log AND in aggregate

## Communication requirement
Talk about emailing every 2 weeks. High level what did I achieve and what the next steps are.

TODO make a template.

## Obsidian Publish
Obsidian publish doesn't natively support

[Support for Dataview JS Snippets · Issue #102 · jackyzha0/quartz (github.com)](https://github.com/jackyzha0/quartz/issues/102)

#choice I am using cloudflare pages as its free and I already have a domain setup with cloudflare.

#choice I am using quartz as its free and self hostable, doesn't require obsidians paid subscription.

### Publish Problems
Publishing straight using quartz has the problem that the dataview plugin isn't executed during publish. So what is published is the raw query rather than the results of the query. Which is not useful for sharing with my tutor.

Thankfully only this week github user saberzero1 published a tool to allow the queries to be run and "baked" into the website.

[saberzero1/quartz-syncer: Markdown publisher for Quartz with Dataview support. (github.com)](https://github.com/saberzero1/quartz-syncer)

## What is the artefact
The core artefact is the specification. Which due to IP reasons cannot be shared in its entirety.
The artefact is:
1) Samples of the redacted specification
2) The code required to create the specification
3) The code required to analyse the specifications
4) The tables/graphs to explain the analysis
5) The analysis discussion

## Importing the data
Exported a bacpac from sql azure. Ran into a problem with importing it locally as my sql server instance didn't have contained database authentication enabled (which we use for replicating the production db / fail overs.)
![Pasted image 20240218184508.png](/img/user/media/Pasted%20image%2020240218184508.png)

[Enable SQL Server Contained Database Authentication (kodyaz.com)](https://www.kodyaz.com/sql-server-2014/enable-contained-database-authentication-on-sql-server.aspx)

fixed by
```SQL
sp_configure 'contained database authentication', 1  
reconfigure
```
```
Configuration option 'contained database authentication' changed from 0 to 1. Run the RECONFIGURE statement to install.

Completion time: 2024-02-18T18:45:49.8038654+00:00

```
## Bibliography
[Using Dataview on Obsidian Publish · joschua.io](https://joschua.io/posts/2023/09/01/obsidian-publish-dataview/)



<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



Tutorial recordings are available at: [TM470-24B Online tutor group room Meeting Recordings | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/connecthosted/viewrecordings.php?id=2217281&group=374810)


![Pasted image 20240211081001.png](/img/user/tutorials/media/Pasted%20image%2020240211081001.png)

The tables are referring to the study guide.

![Pasted image 20240211081150.png](/img/user/tutorials/media/Pasted%20image%2020240211081150.png)
6-7 major tasks, with maybe smaller tasks

missed one
![Pasted image 20240211082008.png](/img/user/tutorials/media/Pasted%20image%2020240211082008.png)
![Pasted image 20240211082018.png](/img/user/tutorials/media/Pasted%20image%2020240211082018.png)
Developing a strategy to X

![Pasted image 20240211082100.png](/img/user/tutorials/media/Pasted%20image%2020240211082100.png)
Data requirements - talk about format. Permissions around use of data.

![Pasted image 20240211082331.png](/img/user/tutorials/media/Pasted%20image%2020240211082331.png)
For each task, consider the associated risk. 
![Pasted image 20240211082638.png](/img/user/tutorials/media/Pasted%20image%2020240211082638.png)
![Pasted image 20240211082743.png](/img/user/tutorials/media/Pasted%20image%2020240211082743.png)
![Pasted image 20240211082937.png](/img/user/tutorials/media/Pasted%20image%2020240211082937.png)
![Pasted image 20240211083021.png](/img/user/tutorials/media/Pasted%20image%2020240211083021.png)Project Plan is a visual representation of the project.

Use Colour Coding. Maybe have a % system. and colour code based on that.
![Pasted image 20240211083532.png](/img/user/tutorials/media/Pasted%20image%2020240211083532.png)
Have lots of little subtasks, makes it easy to carry out.

This is talking about phases and tasks [Planning and Organising a Project | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217339)


![Pasted image 20240211083938.png](/img/user/tutorials/media/Pasted%20image%2020240211083938.png)
Amanda strongly recommends going to the using the library lecture, 28th Febb.

![Pasted image 20240211084118.png](/img/user/tutorials/media/Pasted%20image%2020240211084118.png)

Amanda only teaches TM470.
![Pasted image 20240211084429.png](/img/user/tutorials/media/Pasted%20image%2020240211084429.png)

MS Word can format references for you?!?

![Pasted image 20240211084811.png](/img/user/tutorials/media/Pasted%20image%2020240211084811.png)
Amanada suggests contacting once a fortnight, with a briefing of where you are up to.

YOU ARE MARKED ON IF YOU ARE ENGAGING WITH YOUR TUTOR

![Pasted image 20240211085042.png](/img/user/tutorials/media/Pasted%20image%2020240211085042.png)
![Pasted image 20240211085316.png](/img/user/tutorials/media/Pasted%20image%2020240211085316.png)

![Pasted image 20240211085405.png](/img/user/tutorials/media/Pasted%20image%2020240211085405.png)
The marks are based on the learning objectives on the websites.
![Pasted image 20240211085540.png](/img/user/tutorials/media/Pasted%20image%2020240211085540.png)
![Pasted image 20240211085553.png](/img/user/tutorials/media/Pasted%20image%2020240211085553.png)
![Pasted image 20240211085627.png](/img/user/tutorials/media/Pasted%20image%2020240211085627.png)

Explain the coding approach, its interfaces. etc. Show a section of code to illistrate. Go to a section in the appendix with 1 example. Explain that its a single section and e.g. practicallity. And the rest can be seen here with a github.

They don't check their emails every day. They check them every couple of days.

</div></div>



<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



![Pasted image 20240213103416.png](/img/user/tutorials/media/Pasted%20image%2020240213103416.png)
Blended project, Its going to be a development (make the llm, train etc) and evaluation project
![Pasted image 20240213104257.png](/img/user/tutorials/media/Pasted%20image%2020240213104257.png)
Time for today:
35:20 watching tutorial
4.5 hours of setting up stuff with data view.

# Project Plan
Gives you aims.

![Pasted image 20240221134215.png](/img/user/tutorials/media/Pasted%20image%2020240221134215.png)
Other things: America trip, concerts.



</div></div>


