# Agent Instructions

At the start of each new task or session, read this repository's local instructions and load and read the complete organization rules before doing repository work. First try the current `main` file through the authenticated GitHub API:

```sh
gh api --method GET -H 'Accept: application/vnd.github.raw+json' 'repos/smoke-oasis-lab/agent-rules/contents/AGENTS.md?ref=main'
```

The command does not import the rules by itself; read the complete response. If the API request fails, try the authenticated raw-content URL: <https://raw.githubusercontent.com/smoke-oasis-lab/agent-rules/main/AGENTS.md>. Private raw content requires authorized access; never place credentials in URLs, files, or output. On the configured host, if sandboxed `gh` cannot access the macOS Keychain and reports an invalid token, use the approved external `gh` launch; do not reset the token.

When online sources are unavailable, read the complete offline snapshot at `.agent-rules/AGENTS.md` if present and say that its freshness could not be verified. Do not use an old snapshot while online sources work. If no source works, explain the failure and pause repository work until the rules are available. The consumer repository must ignore `/.agent-rules/` in its root `.gitignore`; put the current private snapshot there for offline access without committing it.

After every successful complete online fetch, refresh this offline snapshot. First confirm `git check-ignore -q .agent-rules/AGENTS.md` succeeds. Write the complete fetched response to a temporary file inside `.agent-rules/`, verify it is nonempty and starts with `# Organization Agent Rules`, then atomically rename it to `.agent-rules/AGENTS.md`. Remove the temporary file on fetch or validation failure and preserve the previous snapshot. Never save or print authentication tokens. Read the full online response before repository work.

For child agents in the same task, provide the already-loaded full rules. Fetch again for every new task or session. Local instructions supplement shared rules; user instructions take precedence, and directory-scoped instructions may define exceptions within their scope.

The shared rules are private. Do not copy their contents into this public community repository. Loading requires authorized read access; do not expose credentials. Agents that read `AGENTS.md` can follow this bootstrap, but a URL cannot force arbitrary clients to load it. Configure other clients to read `AGENTS.md` before work.

## Documentation map

- [`README.md`](README.md) is the community landing page.
- [`profile/README.md`](profile/README.md) is the public GitHub organization profile.
