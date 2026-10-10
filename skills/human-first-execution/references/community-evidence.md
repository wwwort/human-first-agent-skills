# Community evidence behind the skill

This is evidence about user experience and product communication, not proof that one model is universally better. Community posts are anecdotes; official release pages are vendor claims; peer-reviewed work is used for interaction mechanisms.

## What the Opus 5.5 praise actually describes

- Anthropic's September 22, 2026 release says Opus 5.5 communicates more naturally, puts important information up front, is easier to follow in long sessions, and is less likely to use jargon or idiosyncratic phrases. These are the vendor's stated goals and examples, not independent validation: <https://www.anthropic.com/claude-opus-5-5>.
- PCWorld's launch analysis describes the previous Opus as a chatterbox that appended caveats and “loose ends”; its limited test found 5.5 more direct and less likely to leave extra threads: <https://www.pcworld.com/article/3241475/claude-opus-5-5-promises-to-cut-the-chatter.html>.
- A Reddit user describes the appeal as “taste”: human, understandable communication and quick judgment about what is good or bad. Another says 5.5 feels more natural and alive. These are useful descriptions of perceived interaction quality, not population estimates: <https://www.reddit.com/r/ClaudeAI/comments/1wrbwmc/opus_55_is_the_first_model_that_does_everything_i/> and <https://www.reddit.com/r/claude/comments/1wofem6/opus_55_is_like_return_of_my_old_friend/>.
- Hacker News users describe the improvement as more pleasant to read and less “claudish,” while other users in the same discussion still report flowery, hedged, or buried conclusions: <https://news.ycombinator.com/item?id=49803892>. The disagreement is why the skill uses measurable behavior rather than copying a model's persona.

The recurring features are: information order, plain vocabulary, fewer dangling branches, less ritual hedging, less user steering, and clearer state reporting. “Human” here means easy to understand and easy to collaborate with.

## Why GPT/Codex users report high friction

- A long-running Hacker News comparison describes GPT output as more corporate, tangential, and less adult-to-adult, while preferring Claude's concise and on-point replies. This is a user report, not a controlled comparison: <https://news.ycombinator.com/item?id=39735108>.
- A recent r/ChatGPT thread describes everyday answers as excessively cautious and evasive, with uncertainty injected where the user wanted an ordinary judgment: <https://www.reddit.com/r/ChatGPT/comments/1uzslsj/chat_gpt_is_becoming_exceedingly_cautious/>.
- In an OpenAI Developer Community thread, OpenAI support explicitly says it will share feedback about unnecessary handoffs and permission prompts. The thread is evidence of a product complaint and response, not proof that every pause has the same cause: <https://community.openai.com/t/codex-avoids-being-agentic-as-much-as-possible/1371091>.
- A Hacker News discussion of GPT prompts calls out repeated opt-in closers such as “if you want, I can…” and argues that an obvious next step should be taken directly. Other commenters warn that removing all questions can make an agent act before it understands the task: <https://news.ycombinator.com/item?id=44833645>.

## Research basis: the missing layer is grounding

- NAACL 2024 research defines conversational grounding as building shared understanding through clarification and acknowledgement, and finds that LLM generations contain less grounding than human conversations and often presume common ground: <https://aclanthology.org/2024.naacl-long.348/>.
- Microsoft Research's ACL 2025 benchmark finds LLMs were three times less likely to initiate clarification and sixteen times less likely to provide follow-up requests than humans; early grounding failures predicted later breakdowns: <https://www.microsoft.com/en-us/research/publication/navigating-rifts-in-human-llm-grounding-study-and-benchmark/>.
- Frontiers research on virtual assistants finds users prefer repair strategies that address the source of a misunderstanding; indirect actions that shift the burden back to the user are less acceptable: <https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2024.1356847/full>.

The implementation consequence is precise: do not make GPT chatty. Add one low-cost grounding move when it reduces ambiguity, then proceed. This complements directness instead of competing with it.

## Official guidance that aligns with the design

- OpenAI's current GPT guidance acknowledges a tendency toward detailed formatting and recurring phrases, and recommends specifying the needed writing style; it also recommends autonomy prompts that complete authorized work before asking for approval: <https://developers.openai.com/api/docs/guides/latest-model?model=gpt-4.1>.
- The public Codex realtime prompt asks for concise, clear, efficient responses, brief clarification only when materially necessary, no request paraphrase or unnecessary framing, and factual progress updates: <https://github.com/openai/codex/blob/main/codex-rs/prompts/templates/realtime/backend_prompt.md>.

These official materials support using a short, explicit external behavior layer while leaving the model, safety hierarchy, tools, and authorization gates intact.
