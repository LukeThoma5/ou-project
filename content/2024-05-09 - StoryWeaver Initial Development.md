---
date: 2024-05-09
week: 19
draft: true
---
Date: Thursday, May 09, 2024
# Work Undertaken Summary
Create initial version of Story Weaver
Code: [LukeThoma5/StoryWeaver at 20ff6113aabf7d4e7e60430b1110d53b84c66a21 (github.com)](https://github.com/LukeThoma5/StoryWeaver/tree/20ff6113aabf7d4e7e60430b1110d53b84c66a21)

Functionality including:
1) CLI argument parsing
2) Loading and saving of the "database" directory
3) Loading and batching of input user stories
4) Version Control of database directory with git

# Risks


# Time Spent
1hr StoryWeaver
4hr StoryWeaver

# Questions for Tutor


# Next work planned
1) Create AI component for performing interaction
2) Program design diagrams
3) Get llama access
4) Read up on effective prompting

# Raw Notes

# Creating StoryWeaver

## CLI options
Considered both argparse and click. Click seemed to allow for easier non positional arguments so went with click

Made it easier to re-run the script several times by introducing a .env file and loading env variables before running the entry point.

allowing for common arguments like the input and output directory to not be specified every time.

# Loading and saving index file
Could use `json` or `jsonpickle` decided to go with json pickle to allow the index to be saved and restored from index very easily, without marshalling of the types involved.

# Loading the user stories
Couldn't use `jsonpickle` because the json was being created from an external system.
Wanted to avoid the manual creation if I used `json`.
Found these two libraries:
https://pypi.org/project/dataclasses-json/
https://pypi.org/project/dataclass-wizard/

went with dataclasses-json as it had a much bigger following on github.

# UnicodeEncodeError
`'charmap' codec can't encode character '\u200b' in position 48228: character maps to <undefined>`
Some of the pepper cards include non printing characters like the zero-width space. Used a regex in storytransformer to remove any non printing characters.

# Making First or default types work
Was using python3.9, had to bump to 3.12 to be able to make a generic function to keep type safety

```python
def first_or_default[T](list: list[T], predicate: callable) -> T:
    return next(filter(predicate, list), None)
```

# ImportError: cannot import name 'StoryFile' from partially initialized module 'core' (most likely due to a circular import)
Moved StoryFile into its own file and had the 'core' and 'llm' module read them separately