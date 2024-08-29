---
date: 2024-08-21
week: 34
draft: false
---
Date: Wednesday, August 21, 2024

# Time Spent
1.25hr Story Weaver Development
0.5hr EMA Tutorial
1.5 hr Update story weaver class diagram.

# Questions for Tutor


# Next work planned

- [x] Update the model to have HuggingFaceModel in the middle of the chain and add ollama. and the text generation changes.
- [ ] Review the EMA submission details again and start writing the report.

# Raw Notes

## Cleanup
Cleaned up and documented the code for StoryWeaver. All available at:
https://github.com/LukeThoma5/StoryWeaver/tree/EMA


## CLI Interface
```
python3 ./weaver.py --help
Usage: weaver.py [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  add-section           Add a new section to the database
  approve-headings      Approve the headings after potential human...
  document-per-heading  The main entry point, use AI to generate...
  document-per-section  The main entry point, use AI to generate...
  export-book           Export the documentation to a single markdown file
  export-chat           Export conversation of a complete chat that...
  generate-headings     Use AI to generate headings for the documentation
  init                  Initialize the database directory
```

```
python3 ./weaver.py document-per-section --help
Usage: weaver.py document-per-section [OPTIONS]

  The main entry point, use AI to generate documentation from the input folder
  and store it in the database folder, a section at a time

Options:
  --staging_dir TEXT   [required]
  --database_dir TEXT  [required]
  --help               Show this message and exit.
```

# Top Level Diagram
```mermaid
classDiagram
    direction RL
    namespace GitTrackedClasses {
    class IndexFileSection
    class DocumentSection
    class IndexFile

    }
        note for DocumentSection "These classes are serialized\n and saved within the directory\n that is tracked in Git."

    ConversationGenerator .. Message  
    StoryFile .. ConversationGenerator
    ConversationGenerator .. DocumentSection 
    Model .. Message

    class IndexFileSection {
        +str path
    }

    class DocumentSection {
        +str tag
        +str prompt
        +str last_read_story
        +str content
        +str path
    }

    class IndexFile {
        +IndexFileSection[] sections
    }

    IndexFile o-- "*" IndexFileSection 
    DocumentSection .. Database
    IndexFile .. Database    
    

    class Database {
        -Path database_dir
        -Repo repo
        +Database(Path database_dir)
        -index_file_path() Path
        +read_index_file() IndexFile
        +write_index_file(IndexFile index_file)
        +read_section(IndexFileSection section) DocumentSection
        +write_section(DocumentSection document_section)
        +add_section(str tag, str prompt)
        +commit(str message)
    }

    class Message {
        +MessageRole role
        +str content
    }

    Message .. MessageRole

    class MessageRole {
        <<enumeration>>
        SYSTEM
        USER
        ASSISTANT
    }

    class StoryFile {
        +int id
        +str name
        +str content
        +str[] tags
        +str file_name
    }

    note for StoryFile "Representation\n of a single story\n read from the\nfilesystem"

    note for ConversationGenerator "Creates chat for completion by AI"
    note for Model "Consumes chat and generates output"
    


```
# Chat Generation Diagram
```mermaid
classDiagram

 PromptFile o-- "*" PromptFileExample 

    ConversationGenerator *-- PromptFile

        ConversationGenerator <|-- PerHeadingDocumentationConversationGenerator
    ConversationGenerator <|-- PerSectionDocumentationConversationGenerator
    ConversationGenerator <|-- HeadingGenerationConversationGenerator
    

    class PromptFile {
        str system_prompt
        PromptFileExample[] examples
        PromptFileExample test
    }

    class PromptFileExample {
        str prompt
        str[] batch
        str input
        str output
    }
    class ConversationGenerator {
        -PromptFile prompt
        +bool has_system_prompt
        #add_message(Message[] messages, Message message) Message[]
        +read_prompt(Path prompt_path) void
        #_format_batch(str[] batch) str
        
        #_make_example_input(PromptFileExample example)* Message
        #_make_example_output(PromptFileExample example) Message
        #_make_conversation_start(str system_prompt) Message[]
        #_make_user_message(str content_message) Message
    }

    class PerHeadingDocumentationConversationGenerator {
        +PerHeadingDocumentationConversationGenerator(Path prompt_path)
        -make_input_message(DocumentSection section, str current_headings, StoryFile[] batch, str content) Message
        _make_example_input(PromptFileExample example) Message
        -format_documentation_message(str prompt, str structure, str current_headings, str input_documentation, StoryFile[] batch) str
        +make_documentation_chat(StoryFile[] batch, DocumentSection section, DocumentHeading heading) Message[]
    }

    class PerSectionDocumentationConversationGenerator {
        +PerSectionDocumentationConversationGenerator(Path prompt_path)
        -make_input_message(DocumentSection section, StoryFile[] batch, str content) Message
        _make_example_input(PromptFileExample example) Message
        -format_documentation_message(str prompt, str input_documentation, StoryFile[] batch) str
        +make_documentation_chat(StoryFile[] batch, DocumentSection section) Message[]
    }

    class HeadingGenerationConversationGenerator {
        +HeadingGenerationConversationGenerator(Path prompt_path)
        -make_input_message(DocumentSection section, StoryFile[] batch, str content) Message
        _make_example_input(PromptFileExample example) Message
        -format_header_message(str prompt, str input_documentation, StoryFile[] batch) str
        +make_generation_chat(StoryFile[] batch, DocumentSection section, str headings) Message[]
    }

```

# Model Diagram
```mermaid
classDiagram
    direction RL

    class Model {
        +run_messages(Message[] messages)* str
    }

    class BasicModel {
        +bool has_system_prompt
        +BasicModel(bool has_system_prompt)
        _load_model()* void
        _run_messages(Message[] messages)* str
        +run_messages(Message[] messages) str
    }

    class DummyModel {
        +run_messages(Message[] messages) str
    }

    class HuggingFaceModel {
        -AutoTokenizer tokenizer
        -AutoModelForCausalLM model
        +HuggingFaceModel(bool has_system_prompt)
        +get_input_ids(Message[] messages) BatchEncoding
        +get_streamer() TextStreamer
        +extract_output(BatchEncoding input_ids, outputs) str
    }


    class OllamaModel {
        -OpenAI client
        -str model_name
        +OllamaModel(str model_name)
        _load_model() void
        _run_messages(Message[] messages) str
    }

    class Llama3Model {
        +Llama3Model()
        _load_model()* void
        _run_messages(Message[] messages) str
    }

    class Llama3_8B {
        _load_model() void
    }

    class Llama3_70B {
        _load_model() void
    }

    class Llama3_1_8B {
        _load_model() void
    }

    class Phi3Model {
       +Phi3Model()
        _load_model()* void
        _run_messages(Message[] messages) str
    }

    class Phi3_14B {
        _load_model() void
    }

    class Phi3_7B {
        _load_model() void
    }

    class MistralModel {
       +MistralModel()
        _load_model()* void
        _run_messages(Message[] messages) str
    }

    class Mistral_7B {
        _load_model() void
    }

    class Mistral_12B_Nemo {
        _load_model() void
    }

    class Gemma2Model {
       +Gemma2Model()
        _load_model()* void
        _run_messages(Message[] messages) str
    }

    class Gemma2_9B {
        _load_model() void
    }

        Model <|-- DummyModel
    Model <|-- BasicModel
    BasicModel <|-- HuggingFaceModel
    BasicModel <|-- OllamaModel
    HuggingFaceModel <|-- Llama3Model
    HuggingFaceModel <|-- Phi3Model
    HuggingFaceModel <|-- MistralModel
    HuggingFaceModel <|-- Gemma2Model

    Llama3Model <|-- Llama3_8B    
    Llama3Model <|-- Llama3_70B   
    Llama3Model <|-- Llama3_1_8B    
    
    Phi3Model <|-- Phi3_14B
    Phi3Model <|-- Phi3_7B

    MistralModel <|-- Mistral_7B
    MistralModel <|-- Mistral_12B_Nemo
    
    Gemma2Model <|-- Gemma2_9B
```    
