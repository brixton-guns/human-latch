# Human Latch

An agent can fill a wire transfer. The `submit` tool **fails** until a person presses the physical **I have reviewed** button on the page. Then `submit` succeeds. Same session, same DOM.

Not a spec checker. Not a tool catalog. The demo is: agent fills → submit rejected → human clicks → submit ok.

There is **no** WebMCP tool for the latch. The WebMCP tool surface cannot open it. This is not proof of human presence; a computer-use agent controlling the browser may still activate the UI control.

## Live

https://brixton-guns.github.io/human-latch/

## What the agent gets

Registered with `document.modelContext.registerTool` (falls back to `navigator.modelContext`):

| Tool | Role |
|---|---|
| `list_fields` | Field ids on this page |
| `fill_field` | Write one field. Does not submit. Does not open the latch. |
| `get_state` | Latch open/closed, fields, confirmation |
| `submit` | Throws `HUMAN_LATCH_CLOSED` until the human button is pressed |

No iframes. No declarative HTML `toolname` annotations.

## Open it for judges

### ChatGPT in-app browser (site tools)

1. ChatGPT desktop, model that has site tools (not Luna / Enterprise / Edu).
2. Open this URL in the **in-app browser**.
3. Site tools should list `list_fields`, `fill_field`, `get_state`, `submit`.
4. Ask the agent to fill a wire and submit it.
5. Watch `submit` fail. Press **I have reviewed** yourself. Ask it to submit again.

### Chrome flag

1. `chrome://flags/#enable-webmcp-testing` → Enabled → relaunch.
2. Open the live URL.
3. The page prints **WebMCP live** when `registerTool` exists.
4. Use the Model Context Tool Inspector extension, or any agent that speaks WebMCP.

## Run locally

Static files. Any HTTPS origin works (WebMCP wants a real origin).

```bash
python3 -m http.server 8080
```

## License

MIT
