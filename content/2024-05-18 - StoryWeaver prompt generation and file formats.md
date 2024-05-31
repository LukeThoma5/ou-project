---
date: 2024-05-18
week: 20
draft: false
---
Date: Saturday, May 18, 2024
# Work Undertaken Summary
1) Gain access to llama3
2) Read TMA03 requirements
3) StoryWeaver
	1) Change storage from json to xml for better atomic updates and human legible multiline text support
	2) Initial work for adding llama3 support
	3) Initial work to construct a chat history from file, using the same formatting as will be used on the "true" request.

# Risks / Next Actions
1) Get llama3 running locally
2) Create examples for better prompting
3) Diagram storyweaver
4) Read up on effective prompting


# Time Spent
0.75hr TMA03 + EMA reading
0.25hr llama3 access
4hr StoryWeaver Development
0.75hr TMA03 briefing

# Questions for Tutor


# Next work planned
TODO - add some discussion about emissions and how its responsible to re-use an existing foundational model rather than start from scratch.

# Raw Notes
Leaning more towards llama3 due to its better RULER rating and the ability to have a system prompt.

# Development

Broke up the llm file into a sub-folder, so that can have 1 file per llm as each may do things differently.

The llm's need to read in a system prompt and some examples before they can perform their update. This is going to be long and include content over multiple lines so have separated out into its own file to make it easier to track changes just to the prompt.

I have selected to store it in XML as it has best human readable multi-line support:
1) json can do multi-line but its encoded `\n`
2) csv would be brittle

It's making me re-think maybe I should be using xml for the database, and rather than having a separate .md file I could just store the markdown directly in the xml and it would still look okay while enforcing atomic updates.

```json
{
    "py/object": "database.IndexFile",
    "sections": [
        {
            "last_read_story": "001857_000349668_2024_01.json",
            "prompt": "This is the prompt New",
            "py/object": "database.IndexFileSection",
            "tag": "Application",
            "path": "Application.xml"
        }
    ]
}
```

# Problem
The converstation history is specific to the model, as e.g. not everyone has a system prompt. Could put the content in the section.xml but that feels a little muddled / needless repetition.

Proposed solution:
Have a single file for each model, and have it have both a system prompt, and a bunch of example interactions where it has a prompt, a batch, a previous version and the expected output. Can then have the model hydrate the conversation from the examples