# Sync 5/20

Rough plan for the week:

- /file affordance for inserting context
- Make / menu discoverable
  - Ghost text on empty lines via inlay
- Fold it via flaps
- Default system prompt
  - Zed's built-ins - Also configurable in the prompt library
  - User configurable prompts, starred in the prompt library
- collapsed system message containing default prompts (can enable/disable)

Top of mind:

- Zed's shared prompt library
  - The system prompt is controlled by your prompt library, which you can store on disk at a configurable location.
  - Prompts are text and/or native/webassembly modules that produce text, plus an optional metaprompt that controls when the prompt is part of the default system message.  
- You see the entire prompt
- Default system message
  - We use the prompt library to construct a default system message
  - The system message is updated in real time as the environment changes
- Excited to dogfood this with a `prompt_library_path` setting pointing to a directory in our repository.


Review status on:

Nathan: Ship flaps and semantic search results insertion

- Resolve ambient context  
  /file assistant_panel.rs
  - slash command for inserting files and file excerpts
    - Text represented as an inlay
    - Use "flaps" to insert a custom foldable region around the inlay with a custom gutter decoration
  as inlays/blocks/flaps

Antonio
  - Ship applying conversation -> buffer edits
  - What's next?
Marshall: MVP for dynamic prompts via extension API
  - Not sure how baked we'll want this to be before we ship it, since extension API has a hard contract. We're not making any other extension API changes at the moment, so we can let it sit and bake.
Nate:
  - Allow prompts to be editable/revertable from library, allow creating new prompts.
  - Remove the concept of "activating" prompts, instead make clear "add to default prompt"
Max: add temperature control, help with dynamic context

---

- v System
  :file: baoeusth
  :file: aoeusth

  Read-only snippets

  /search using a multibuffer

  ```a (anchor range into some excerpt)

  bla

  ```

  ```b

  ```

  ```c

  ```

  Change bla to blu

  ```a'
  blu
  ```


# Sync 5/17

* *Solving our own meta-problems* - When solving complex AI problems, what tools do _we ourselves need_ to efficiently build with AI? If we build that, we work more efficiently and build stuff other people will probably also want.
* Demo apply changes
* Nate design review
  - / menu
* System prompts
    * introduced a system prompt for assistant edits, how do we present it
* Prompt Library
    * Need to be able to persist the state of the prompt library
    * Use project info to conditionally apply activated prompts based on language or deps
    * (Nate) I'm really enjoying working on this, and would love to do the work to make prompts creatable & editable in the prompt manager – But it'll take a bit of time. Let's chat if it's worth me continuing to work on this.

# Roadmap: AI

Hosted AI Offering Launch: June 5th, 2024

Team Leads: Antonio, To Be Hired

In progress

- Meta problems - Things slowing us down in our experimentation:
  - Fix our rate limiting so that all Zed employees go through zed.dev
  - Adjust temperature in the UI (nate - happy to riff on in-ui controls, there are some good example patterns we can pull from)
  - Better error reporting from Anthropic API - What's happening?
  - Make assistant editor collaborative
  - Explode system prompts and ambient context for manual editing
- Semantic search
  - Flaps API - Fold away context, etc with custom indicators @nathan
- Apply edits – @as-cii and @maxbrunsfeld
  - Autoscroll to the first user message (below auto-inserted system message)
  - Place ambient context icons in toolbar to the left of "insert context"
  - Remove magic wand and add a "Send" button on the bottom right
- Ambient project context
  - "Summarization level"
  - We want it to be controllable




- Prompt
  - Text that you can insert into your doc with autocomplete.
  - Can be dynamic - WASM or native functions that take input and output text.


System

--------


]













On Deck  

- / Menu  
- Accept/reject text transformations
- Create new files
- Ambient context
  - Terminal
  - Project context - File tree, Rust dependencies @marshall
  - Summarization / getting more control
- / Autocomplete menu - @nate's vision
  - Semantic search
  - Fuzzy searching your prompt library
  - File tree with fuzzy patterns
  - Documentation
  - Crawl a site
- System context
  - Zed system prompts
  - "Snapped rubber band" scrolling - (I think the short term version of this could just be we start the list scroll at "you" but there is content above)
  - Autocomplete from prompt library

- Sanitize messaegs  for Anthropic Claude
  - No empty messages, strict alternation between User and Assistant

- Semantic search UI embedded in the document
- Code rendering
  - Close open markdown code blocks at the end of message
- Semantic search text driven UI



- Hide context buttons that don't work
- Enable the context by default in the autocomplete
- Apply suggested edits to buffer
  - Append "apply edit" suggestion to end of line when cursor is inside the code block.
- Make context editor collaborative
- Saved prompt library
  - Can we get context loading from .config/zed/contexts? (I started on this - nate)
  - Metaprompt – We can associate a prompt in the library with natural language expression of when it should be enabled based the current context.
- Language-specific project context
  - Load dependency-specific prompts into our context.
- Project specific prompts in `.zed`, provided by a team/project
- Use feature flags liberally. If you can't get enough flexibility to experiment it's fine to fork.



-----------------

https://www.figma.com/design/1Dv3XRTnJU2IhIpmuY3kzP/ai_refinement?node-id=13-13&t=nAVioRnFIejBxdHG-11

- Ambient context (included in first system message on each request)
  - Terminal
  - N most-recently-focused open files
    - Diagnostics
    - Related excerpts
    - Remove old file contexts
  - Project diagnostics (Alert icon or something like that)
  - Project directory tree summary
  - Automatic summarization by level
  - Snapshot ambient context - Edit it as text
- Injections
  - Search
    - Insert a search prompt for every cursor on an empty line
    - Annotate the region with a fold decoration
      - Custom fold affordance in gutter > Magnifying glass
      - Optional fold guide (thin line that extends from icon to bottom of fold)
      - Optional custom element to render at the end of the first foldable line
    - Run query by hitting enter within the search prompt
    - Query results are rendered as portals into the original text
    - Each result is folded by default with its search result fold decoration
  - Selected text
    - Can be injected as portals from the current selection
    - Custom fold decoration    
  - Documentation
    - Fast, high quality text for popular languages, starting with docs.rs
    - Best effort for arbitrary URLs via crawler
    - When you insert it, you get an empty line with an autocomplete
      - The contents of the line are a fuzzy query which navigates the autocomplete
      - doc/ru/foo <- fuzzy with substring search, or maybe a fast model call
- Special handling for language model output
  - Run scripts
    - Shell, runs in the terminal like a task
    - Rendered for fenced blocks that start with ```sh
  - Apply generated code to codebase
    - If the editor generates code that identifies a specific
- Inline assist
  - Always link to the active context
  - Improve styling
  - Multibuffer
  - Inline assist in the assistant panel
  - Multiple cursors / selections spawn parallel generation from the same prompt
  - Inline assist in the terminal

## Meeting

- What has been built, what is promising?
  - Attachments
    - Custom Prompt
    - Other buffers
  - Multibuffer derived from semantic search
    - We are really good at non-local editing  - Injecting portals into the conversation
- Max
  - Top priority: Ask a terse question, get a multi-buffer
    - Stream the tool call input
    - How do I make worktree scanning lazier?
      - Semantic search runs
      - Tab opens, excerpts are popping in and being written.

- Recent assistant 1 thoughts / demo
- Philosophy of how we're solving problems
- We have to use what we're building? Pet projects.
  - If we can learn to generate code more effectively than we can write it today manually, we win in a world where language models are becoming exponentially more powerful.
  - Pick a feature or a bug, commit zero non-generated code solving it.

---

Nate's raw thoughts from the meeting/demo this morning:

- what do we need to make this thing good for rust?
- can we prove it out by teaching it to write gpui?
- how much can we do by gluing static and dynamic prompts? (looks like we might be most of the way there)
- anything that blocks us from using it daily we should push to further in the project (part of the problem with a2 was there was so much work to be done before we could even use it)

- is branding it the right approach? or should we just embed it into the dna of zed? (inline assist = refactor or transform?)
- what does it look like for the community to contribute contexts to this?

- dont plan backwards from a date
- each monday meeting decide what else we need before the [ team | power users | all users ] can use it


## Next steps

- Rate limiting around the semantic index (zed cloud embeddings)
  - UX for when a hit rate limit
    - Use same UI as consent figma below (marshall started on this)
  - detailed message on rate limit error surfacing rate limit state
  - Telemetry to help us understand what a reasonable rate limit would be

- Saving conversations
 - Bring over the assistant1 functionality

- Port over quote from selection from assistant1
  - Inject into user message directly

- When the project index is enabled, encourage the model to use it in the system prompt
  - Either system prompt or we force the tool call by swapping from `auto` to `[tool_call_name]` in the submission



- Introduce Attachment for custom prompt from settings  [](https://www.figma.com/file/ZlDLXq7YeXghqzo0PPMZiR/Assistant-2?type=design&node-id=169-1557&mode=design&t=riCSiSW3wvnQQvZ0-11)

- Add context controls to the composer (with tooltip)
    - Project diagnostics
    - Terminal history
    - Custom Prompt from Settings

- [@antonio @nathan] Rework markdown
  - Use Markdown view in assistant chat
  - Allow selected text to be copied
  - Style inline code differently from code blocks
  - Improve code block rendering in rich text

Attachments
  - Current buffer
  - Project directory structure outline
  - Project diagnostics
  - Terminal history
  - Custom Prompt from Settings

- Ask for consent before populating semantic index for project
   [Figma](https://www.figma.com/file/ZlDLXq7YeXghqzo0PPMZiR/Assistant-2?type=design&node-id=92-5943&mode=design&t=riCSiSW3wvnQQvZ0-4)

- Chat history UI

- Tool Call Progress UI
  - [](https://www.figma.com/file/ZlDLXq7YeXghqzo0PPMZiR/Assistant-2?type=design&node-id=169-1042&mode=design&t=riCSiSW3wvnQQvZ0-11)
  - `trait` on the LanguageModelTool to emit some signal with strings
  - When the assistant is calling a tool, inline the function call status as if it's the model "saying it" within the chat
  - We want some way to progressively update the status of executing some long running tool

- Improve visibility into errors in indexing
  - How do we handle the following errors
    - Rate limiting
      - Retry... but we obviously have to wait
      - Can we avoid this?
    - Network disconnection
    - Embedding provider errors (500s from OpenAI, 400s, etc.)  

- Allow messages to be selected from the keyboard
    - Pressing `up` when on the first line of the editor should select the message above the composer, and have a selected style 💯
    - Pressing `cmd+down` instantly focuses the composer
    - Pressing `e`/`enter` or double clicking makes this message editable
    - Pressing `c` collapses the message (or clicking the line in the gutter)

- Render a scrollbar for the assistant
- Feature flag for the new assistant to bring in more testers

---

Feedback from Wil

- "Open all the files that have changed since HEAD"

-----------------------------------

## Features we want to ship

We've tried to organize everything we'd ideally ship by category rather than priority. We may not get to all of this before launch.

### Assistant panel

#### Tools

- Queries:
  - List a directory
  - Read file
  - Diagnostics
  - Terminal Output
  - Go-to-definition
  - Find-all-references
- Actions:
  - Edit current selection
  - Edit files (show edits in multi-buffer)
  - Open excerpts
  - Run test
  - Save files (to update diagnostics)
  - Zed command palette actions
  - Suggest terminal commands
- Display affordances
  - Display an excerpt from the codebase

#### Automatic context

Custom system message prompts that are dynamic in Zed:

- Open Editors Summary
  - All the paths of the currently open files
  - Current active editor
  - "Rollup view" - "user's cursor is here"
- Summary of current file
  - Outline of overall file
  - Full code surrounding newest cursor
- Project diagnostics
- Edit history
- Git status
- Summary of project directory structure
  - Directories to depth N
  - More detail for directories containing active file / open files
- Terminal history

#### Manual context - Cursor-style @-mentioning

- URLs
- Documentation for framework, library, crate
- User-provided skills/primers
  - "Pull in the GPUI primer"
- Particular files or glob patterns

#### Assistant UX

- Show code in a monospace font
- When the assistant shows an excerpt from the codebase, provide an affordance to jump there (allow multi-buffer style inline edit?)

### Inline assistance

- Ctrl-enter in buffers
  - Make it multicursor
  - Reference chat by default
  - Record a record of doing a ctrl-enter in the chat
  - Provide more awareness of what changed
    - Leave a diff in the wake of rewrites as it finishes lines?
    - Leave a block decoration?
    - Highlight what the AI inserted or changed by shifting color slightly?
    - Accept / reject to dismiss the above?
- Fix error affordance in diagnostics
- Enable ctrl-enter in terminal

### Copilot style autocomplete

- UX for selecting which autocomplete provider to use
- Finish supermaven integration
- Build our own based on a fast general purpose model
  - Suggest non-local edits

### Misc

- Make the command palette more intuitive by calling a model
- Allow users to edit system prompts
- Make it all work on remote projects

### Logistics

- Build a free-trial / billing flow
- Make this work with Claude in addition to GPT-4
- UX for opting into project indexing (we need consent)
- Allow user to work through local providers (with API keys) in addition to hosted provider

----- Notes on a conversation between Marshall and Nathan

How do we present the conversation to the user?

  The story we're presenting is a dialog between user and assistant.

  With each historical user message, what context did we send to the model at the time that user message was initially sent?

  With each historical assistant message, what tools did the assistant call and what were the results?

When the user hits send, how do we transform what the user is seeing in assistant pane to JSON data to pass to the model?

  Even though we display the context sent with each historical user message, we don't want to send this context again for the latest invocation.

  Instead, we want to look at the options the user has toggled on the latest message's composer and use them to construct a System message that precedes the entire conversation history and orients the model with a summary of the situation in the editor at the time the message was sent.

  Based on the users options, we take a snapshot of context that we attach to their message for historical reasons... but it also needs to get baked into the system message to guide the model's behavior.


  Context:
    System message
    Chat history (User & assistant messages)

  Latest user message


User message - Drafting
  - Summary of the context sent
Assistant message reply
User message
System message
Assistant message reply

---

## Nate's Ship Wishlist

- Go out with a bunch of contexts that people can add to their assistant
  - maybe focus on rust?
- Update the welcome page
