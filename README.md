# renovate-config

Shared Renovate preset for the Tracearr repos.

`default.json` holds the house style: schedule, cooldowns, commit message format,
the automerge block, the GitHub Actions and Docker groups, and the major-update
assignee. Repos extend it and declare only their own package groups.

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>Tracearr/renovate-config"],
  "packageRules": [
    // repo-specific groups
  ]
}
```

## Ordering

A repo's own `packageRules` are evaluated after this preset's, and for any field
both set, the later rule wins. That is how a repo pulls a package out of a broad
group defined here — declare it in a narrower group locally and no exclusion list
is needed on either side.

For example, this preset groups every `@types/*` into "type definitions". A repo
that wants `@types/react` to move with React declares its own React group; the
later rule takes it.

## Consumers

- connorgallopo/Tracearr
- Tracearr/Mobile-App
- connorgallopo/tracearr-docs
- connorgallopo/tracearr-site
- Tracearr/discord-bot

## Validating a change

```bash
npx --package renovate@latest renovate-config-validator default.json
```

Renovate resolves the preset fresh on each run, so a change here reaches every
consumer on their next scheduled run. There is no version pin.
