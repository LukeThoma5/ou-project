---
{"publish":true,"path":"2024-02-21 and -02-26 - TMA01 Execution.md","permalink":"/2024-02-21-and-02-26-tma-01-execution/"}
---

Date: Wednesday, February 21, 2024
# Work Undertaken Summary
- Setup Remote Desktop to Server
- Review Google Gemma
- Tasks list
- Estimate Tasks list
- Create project Schedule
- Research, Choose and justify lifecycle
- Review in depth TMA01 requirements

# Problems encountered and how you overcame them
Mostly Assignment Work this week.

# Time Spent
| Top Level                                | Second Level                                                                     | Time               | Progress (%) this week est |
| ---------------------------------------- | -------------------------------------------------------------------------------- | ------------------ | -------------------------- |
| [[Environment Setup\|Environment Setup]] | [[Tasks/Environment Setup/Server OS Install\|Server OS Install]]              | 30 minutes         | 5                          |
| [[Recurring Tasks\|Recurring Tasks]]     | [[Tasks/Recurring Tasks/Tutorials\|Tutorials]]                                | 30 minutes         | 5                          |
| [[TMA01\|TMA01]]                         | [[Tasks/TMA01/Project Schedule\|Project Schedule]]                            | 5 hours            | 60                         |
| [[TMA01\|TMA01]]                         | [[Tasks/TMA01/Lifecycle Selection\|Lifecycle Selection]]                      | 3 hours            | 60                         |
| [[TMA01\|TMA01]]                         | [[Tasks/TMA01/Write Assignment\|Write Assignment]]                            | 1 hour, 36 minutes | 5                          |
| [[Research\|Research]]                   | [[Tasks/Research/Complete a literature search\|Complete a literature search]] | 15 minutes         | 5                          |
| [[Recurring Tasks\|Recurring Tasks]]     | [[Tasks/Recurring Tasks/Bi Weekly tutor Updates\|Bi Weekly tutor Updates]]    | 30 minutes         | 5                          |
| [[TMA01\|TMA01]]                         | [[Tasks/TMA01/Log Book\|Log Book]]                                            | 1 hour             | 10                         |


# Questions for Tutor
N/A
# Next work planned

4) Add risk management to template
6) Risk Register
7) publish blog for tutor and email

# Raw Notes


## Remote Desktop
All my research and notetaking occurs on my laptop, which is not capable of running the LLM. To be able to easily context switch during the project I have setup remote desktop functionality to allow me to use the server as if it was another window.

### Problems encountered
Options tried / considered:
xrdp - After login gives just blue screen [Xrdp - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/Xrdp)
FreeRDP - Far too much configuration to just get it working [FreeRDP-Manuals/Configuration/FreeRDP-Configuration-Manual.markdown at master · awakecoding/FreeRDP-Manuals · GitHub](https://github.com/awakecoding/FreeRDP-Manuals/blob/master/Configuration/FreeRDP-Configuration-Manual.markdown)
Parsec - Machines wouldn't mind each other on the network [AUR (en) - parsec-bin (archlinux.org)](https://aur.archlinux.org/packages/parsec-bin)
Solution:
Solved by using rustdesk - [RustDesk – The Open Source Remote Desktop Access Software](https://rustdesk.com/)

# Reading
#research
[Welcome Gemma - Google’s new open LLM (huggingface.co)](https://huggingface.co/blog/gemma)

New LLM from google, appears to work almost as well as llama2's 70B chat variant. while being significantly smaller. Could be good to use as the base / comparison. Could be good to iterate with or maybe minstrel?

maybe try phi-2 from microsoft? [microsoft/phi-2 · Hugging Face](https://huggingface.co/microsoft/phi-2)

## Creating a project plan
resource map:
[Resource Map | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217310)

Allocate about 10 hours per week.


Unit of time - Weeks

Setting up workbook with: [Conditional formatting with formulas | Exceljet](https://exceljet.net/articles/conditional-formatting-with-formulas)

## Task List
Most projects can normally be broken down into phases such as:

- concept development
- planning
- research
- design
- development
- testing
- evaluation
- implementation
- writing of report.

Have top level tasks for the TMA's. E.g each TMA can be a phase.

# Possible title: Developing an AI system to transform User Stories into a Software Specification

## Task List

### TMA01

- Recurring Tasks
	- Bi Weekly tutor Updates
	- Tutorials
- TMA01
	- Initial Ideas
	- Project Proposal
	- Project Schedule/Plan
	- Resources and Skills
	- Risk Register
	- Lifecycle Selection
	- Logbook Setup
	- Blog Setup
	- Write Report
- Research
	- complete a literature search
	- analyse literature
	- complete review of literature.
- TMA02
	- legal, social, ethical or professional issues and equality, diversity and inclusion
	- risk assessment
	- reflection
	- Write Report
- TMA03
- EMA
- Design
	- Top Level Design Research
	- Top Level Diagram
	- Data Transformation Design
	- Specification Generator Design
- Environment Setup
	- Server OS install
	- Ollama install
	- Jupiter Notebooks
	- Docker image (reproducible)
	- Pandas / Seaborn
	- LangChain install
- Data Transformation
	- Retrieve Database
	- Create program to transform data for LLM consumption
	- Tune output to LLM
- Build Specification Generator
	- Setup LangChain + Ollama integration
	- Read User Stories and feed to single LLM
	- Review LLM output
	- Tune LLM interaction (System message / process)
	- Make generic to run against multiple LLM's
- Select LLM's to benchmark
	- Review current landscape (benchmarks)
	- Review licences and obtain models
- Benchmark LLM's
	- Run against different LLM's and fixing minor issues
	- Specify Marking Criteria
	- Mark each LLM and enter data into spreadsheet
- Analyse LLM performance
	- Import data into pandas
	- Analyse data
	- Create charts
	- Writeup recommendations and interpretation

TODO continue from here: [Planning and Organising a Project: 4.3 Tasks | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217339&section=4.3)
Continue filling out the task list.


# LO9
The lifecycle selection is very important for the marking criteria, and feeds into the appropriateness of the schedule that I create. Should be a priority to complete and justify the lifecycle selection.

# Legal, Social, Ethical and Professional issues
More information available at: [Legal, Social, Ethical and Professional issues | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2254931)

Possible considerations:
- IP issues surrounding the ownership of the specification / design.
- Legal use of the AI - e.g. okay for research use. E.g. the licence of the AI
- Ethical issues around AI
	- Replacement of jobs (PO / support staff)
	- Accuracy of AI output and any implications of its inaccuracy (maybe talk about the airline held to the output of the AI model)
	- Possible issues around equality/diversity/inclusion based on the use of AI. Like potential for the AI to assume / reinforce that a truck driver is a man and a CS agent is a woman.

# TMA01 Checklist
- a.Identifying the goals and content of your project.
- b.Starting to select and evaluate relevant information sources that describe related work and point to possible methods to be used.
- c.Identifying resources (especially data, access to people, etc.) that are crucial for success and assured yourself that these will be available when needed.
- d.Identifying and evaluating your own skills and knowledge that are crucial for the success of this project. Identifying essential skills that you lack and starting to develop them.
- e.Choosing an appropriate project lifecycle model and starting to plan and schedule the work required based upon this.
- f.Undertaking some exploratory work to begin the project work.
- g.Reflect on progress to date.

We suggest you organise your TMA under three main headings:

- Preparation and planning
- Project work
- Review and reflection.

https://learn2.open.ac.uk/mod/oucontent/view.php?id=2254953

Your schedule should be consistent with the project lifecycle you have chosen, so if an iterative lifecycle has been selected, your tutor will expect to see iterations in your schedule.


# Project Work
Make a diagram showing how the different components will interact.

Database, c# data manipulator, python + langchain workflow, ollama + llama2.  Evaluation -> excel -> pandas+seaborn investigation.

# Choosing a lifecycle
[Choosing a Lifecycle Model | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217314)

When discussing the choice of lifecycle refer back to [Choosing a Lifecycle Model: 2 Project lifecycle models | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217314&section=2)

## Classic Waterfall
Royce, W.W. (1970) ‘Managing the development of large software systems’, _Proceedings of the IEEE WESCON_, vol. 26, pp. 1–9.

![waterfall.png](/img/user/media/waterfall.png)

Waterfall is inappropriate because:
- The project is in an unfamiliar domain, so upfront analysis and design aren't possible
- It is not routine, it is novel. I am trying to produce something new and so there is not previous projects to reference
- The project needs a level of iteration. Specifically with the design of the the data manipulation / presentation, system prompt.

## Iterative waterfall model

While it allows for iteration and for backwards steps, it prioritizes minimizing backwards stepping, especially over more than 1 step. Which does not match the fact that I am going to need to do many loops of design/implementation/evaluation.

![iterative waterfall.png](/img/user/media/iterative%20waterfall.png)

## Prototyping
Could be useful, but incremental delivery might be a better shout.

"Evolutionary prototyping is one form of incremental delivery (see Section 2.3), but in the case of incremental delivery the overall design and planning for the product are done up front, while in evolutionary prototyping they are usually not."

- evolutionary prototyping -  the product emerges through a series of prototypes that gradually improve in quality and scope
- throwaway prototyping - prototype is developed as a stepping stone to a final product

## User-centred lifecycle model
![user-centred-lifecycle.png](/img/user/media/user-centred-lifecycle.png)

While building an incrementally improved prototype fits my expected outcome, I don't think "discovering requirements" quite fits the iteration I will be doing. The iteration is more likely to be guiding the AI on important aspects / unimportant aspects.

## Incremental delivery and scrum

The subtle but important distinction between incremental and iterative development is that the goal of an _incremental_ project is to develop an increasingly elaborate output – one with increasing capabilities – whereas an _iterative_ model strives to develop an increasingly correct output – i.e. one that is less error-prone or meets stakeholders’ expectations more thoroughly.

Therefore my lifecycle should be **iterative** as its building a system to create an ever more 'useful' specification. E.g. the output gets increasingly better rather than the workflow getting more capabilities.

A large part of the work will be tuning rather than incremental features.

![scrum-lifecycle.png](/img/user/media/scrum-lifecycle.png)

The project can only be split into a couple of pieces, these pieces can't be enhanced only tuned to produce a better outcome. therefore the result of each sprint wouldn't be a potentially shippable increment and so 

## Spiral Model
Consideration of risk can be built into an iterative lifecycle model by assessing project risk at the end of each iteration and then deciding which aspect of the product to address in the next iteration. This approach was originally suggested by Barry Boehm (1988), based on his experience with large-scale software projects, and he dubbed it the **spiral model**.

Boehm, B.W. (1988) ‘A spiral model of software development and enhancement’, _Computer_, vol. 21, no. 5, pp. 61–72.

- It allows many lifecycles to be modelled within the spiral lifecycle, depending on the current highest risks.

- It fosters the development of specifications that are not necessarily uniform, exhaustive, or formal, in that they defer detailed elaboration of low-risk software elements and avoid unnecessary breakage in their design until the high-risk elements of the design are stabilized.
- It incorporates prototyping as a risk reduction option at any stage of development. In fact, prototyping and reuse risk analyses were often used in the process of going from detailed design into code.
- It accommodates reworks or go-backs to earlier stages as more attractive alternatives are identified or as new risk issues need resolution.

### Disadvantages:
The three primary challenges involve:
- matching to contract software - not an issue as is for me
- relying on risk-assessment expertise
- the need for further elaboration of spiral model steps


[Risk-driven development with the spiral model - LogRocket Blog](https://blog.logrocket.com/product-management/risk-driven-development-with-the-spiral-model/)

### Steps of spiral
1. ****Objectives determination and identify alternative solutions:**** Requirements are gathered from the customers and the objectives are identified, elaborated, and analyzed at the start of every phase. Then alternative solutions possible for the phase are proposed in this quadrant.
2. ****Identify and resolve Risks:**** During the second quadrant, all the possible solutions are evaluated to select the best possible solution. Then the risks associated with that solution are identified and the risks are resolved using the best possible strategy. At the end of this quadrant, the Prototype is built for the best possible solution.
3. ****Develop the next version of the Product:**** During the third quadrant, the identified features are developed and verified through testing. At the end of the third quadrant, the next version of the software is available.
4. ****Review and plan for the next Phase:**** In the fourth quadrant, the Customers evaluate the so-far developed version of the software. In the end, planning for the next phase is started.
[Spiral Model - Software Engineering - GeeksforGeeks](https://www.geeksforgeeks.org/software-engineering-spiral-model/)

### Reasons to choose spiral
1) de-risks early, important for ensuring continuous progress towards the objective
2) is appropriate for internal projects
3) My project is high risk and has low risk aspects that can be easily deferred
4) Flexible (any other model can fit within it)
5) Iterative (not necessarily incremental)
6) Focus on prototypes

## Model Choice
"Regarding your choice of project management approach, if you think of the project management approach as being at a more abstract layer of the fractal, and the process model at a more concrete layer, then you can see that they need to be compatible but don’t need to be the same. For example, if you choose a predictive project management approach you could still choose an incremental or iterative process model for your implementation stage."

Spiral best matches my development philosophy and the requirements of the project.

## Risk Assessment
[Choosing a Lifecycle Model: 3.2 Risk assessment | OU online (open.ac.uk)](https://learn2.open.ac.uk/mod/oucontent/view.php?id=2217314&section=3.2)

- **low impact:** has negligible effect on the project, e.g. a delay of a few days
- **medium impact:** has considerable effect on the project, but it is still likely to succeed
- **high impact:** the project’s success is threatened.

- **low likelihood**: it would be considered surprising if it occurred or proved to be the case
- **medium likelihood**: it would be disappointing but not surprising if it occurred
- **high likelihood**: it will very probably prove to be the case.

![Risk Combination Table.png](/img/user/media/Risk%20Combination%20Table.png)

## Project Schedule
Have completed work schedule. Have left some slack space (about 5 weeks worth) for the inevitable slippage of the project.