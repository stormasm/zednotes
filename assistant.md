
#### How do I turn off the OpenAi Messaging

- [discord](https://discord.com/channels/869392257814519848/1250470360139300934/1268280325025304688)

```rust
"features": {
    "inline_completion_provider": "copilot"
  },
  "assistant": {
    "version": "2",
    "enabled": false
  },
```

### Legacy

I haven't compared all of the code that was changed with what you've done, but the "assistant2" has effectively been "killed off."

We decided to improve the original assistant, rather than have a new assistant that feels more like a chat service. We've come to really love the simplicity of the original assistant, where all of the text can be easily edited.

That being said, we are currently working to make the original assistant much more capable (being more aware of your codebase, being able to create edits that can be directly applied to your source code in the format that Zed understands, etc.)

A QoL thing I'm excited about is that the assistant will have a prompt library. A place where you can store your prompts and pull them up easily when starting a new convo. We already have an MVP, but we will be polishing the experience up.

- [Remove wiring for assistant2](https://github.com/zed-industries/zed/pull/11940)
- [discord ref](https://discord.com/channels/869392257814519848/873293828805771284/1242209152806420603)
