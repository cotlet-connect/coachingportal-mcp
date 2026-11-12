# CoachingPortal MCP server for ChatGPT and Claude

Connect CoachingPortal to ChatGPT, Claude and other AI agents through Cotlet. Work with client check-ins, workout templates and training programs in your own signed-in account. Cotlet is independent and not affiliated with CoachingPortal.

## What you can ask

> List pending client check-ins for this week.

> Create a private workout template from the exercises, sets and reps I provide. Ask me before saving.

> Prepare feedback on the check-in I select. Ask for my approval before sending it.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its CoachingPortal tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"coachingportal": {"command": "python3", "args": ["/absolute/path/to/coachingportal-mcp/coachingportal_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t coachingportal-mcp .
docker run -i --rm -e COTLET_API_KEY coachingportal-mcp
```

Tools: `coachingportal_guide`, `coachingportal_status`, `coachingportal_open`, `coachingportal_read`, `coachingportal_click`, `coachingportal_type`, `coachingportal_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 coachingportal_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 coachingportal_agent.py status    # is CoachingPortal ready in your Cotlet.dev account
python3 coachingportal_agent.py guide     # CoachingPortal screens and sign-in link
python3 coachingportal_agent.py read      # open CoachingPortal, read the page, close the browser
python3 coachingportal_agent.py tools     # list Cotlet.dev tools
python3 coachingportal_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from CoachingPortal users

**How do I connect CoachingPortal to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to CoachingPortal once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your CoachingPortal account through Cotlet, in their phone apps too.

**What can ChatGPT do in CoachingPortal?**

With Cotlet, ChatGPT, Claude and other AI agents handle jobs like these in CoachingPortal: create workout template; assign workout program; review submitted check-ins. You ask in plain words, and anything that reaches other people waits for your OK first.

**Can ChatGPT create program template in CoachingPortal?**

ChatGPT saves a private CoachingPortal workout template from your workout days, exercises, sets, reps and loads. Saving the template does not assign it to a client.

**Does CoachingPortal have an API?**

CoachingPortal publishes no public API. Its FAQ, help center and pricing pages provide no developer documentation or self-serve API key. CoachGPT is built into CoachingPortal and is separate from an external ChatGPT or Claude connector.

**Is Cotlet affiliated with CoachingPortal?**

No. Cotlet is independent and not affiliated with CoachingPortal.

## Find it on

- [CoachingPortal on Cotlet](https://cotlet.dev/integrations/coachingportal-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/coachingportal-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=coachingportal

Request access: https://cotlet.dev/signup?app=coachingportal&utm_source=github&utm_medium=readme&utm_campaign=coachingportal
