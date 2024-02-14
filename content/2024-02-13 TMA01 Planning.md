---
date: 2024-02-13
week: 7
time:
  - task: "[[Log Book]]"
    time: 7.5 hours
    progress: 5
  - task: "[[Tutorials]]"
    time: 3 hours
    progress: 0
---
Date: Tuesday, February 13, 2024
# Work Undertaken Summary
- Document Logbook choices
- Setup Logbook
- Setup Timesheet + reporting

# Problems encountered and how you overcame them
Had to learn how DataView works. Especially around the complex object for the time property. Was able to get it to work using the examples provided by [Dataview (blacksmithgu.github.io)](https://blacksmithgu.github.io/obsidian-dataview/)
[seburbandev/obsidian-dataview-cheatsheet: This cheatsheet provides a handy reference guide for writing powerful queries using the dataview plugin in Obsidian. (github.com)](https://github.com/seburbandev/obsidian-dataview-cheatsheet)

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


# Next work planned


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


## What is the artefact
The core artefact is the specification. Which due to IP reasons cannot be shared in its entirety.
The artefact is:
1) Samples of the redacted specification
2) The code required to create the specification
3) The code required to analyse the specifications
4) The tables/graphs to explain the analysis
5) The analysis discussion

![[2024-02-11 TMA01 Tutorial]]

![[2024-02-13 Welcome Tutorial]]