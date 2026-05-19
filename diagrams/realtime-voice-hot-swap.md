# Realtime Voice Hot-Swap

```text
Start realtime interview
        |
        v
Open Amazon Nova Sonic session
        |
        v
Stream audio and receive interviewer responses
        |
        v
Track turn history and accumulated interview context
        |
        v
Soft safety threshold before provider limit
        |
        +-- if silence detected --> hot-swap now
        |
        +-- if no silence -------> keep waiting briefly
        |
        v
Hard safety threshold before provider limit
        |
        v
Force hot-swap before upstream session limit
        |
        v
Close old session -> refresh auth token -> open new session
        |
        v
Replay conversation history with continuation instructions
        |
        v
Continue interview without re-introduction
```

## Design Notes

- The user should experience one continuous interview even if the underlying realtime model session changes.
- Continuation prompts must explicitly prevent repeated greetings or scenario resets.
- Token refresh is part of reconnect reliability because realtime auth can expire during long sessions.
- Watchdog logging helps detect silent reconnect failures.
