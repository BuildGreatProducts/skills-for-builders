# Skills for Builders

Open-source [Agent Skills](https://docs.claude.com/en/docs/claude-code/skills) for people building products with AI. Each skill is a folder with a `SKILL.md` that tells a coding agent like Claude Code how to do one job well, from start to a checkable finish.

## Skills

| Skill | What it does |
| --- | --- |
| [app-teardown](app-teardown/SKILL.md) | Screenshots every screen of your app, critiques each screen and flow for UX, conversion, retention and product, lays each flow out on a `/design` canvas with the critique beside it, and writes a ranked report to `docs/teardown/`. Never edits app code. |

More skills are on the way.

## Install

Clone the repo:

```bash
git clone https://github.com/BuildGreatProducts/skills-for-builders.git
```

Then copy the skills you want into your Claude Code skills folder. For every project:

```bash
cp -r skills-for-builders/app-teardown ~/.claude/skills/
```

Or for one project only, from that project's root:

```bash
mkdir -p .claude/skills && cp -r /path/to/skills-for-builders/app-teardown .claude/skills/
```

To pick up updates with `git pull`, symlink instead of copying:

```bash
ln -s "$(pwd)/skills-for-builders/app-teardown" ~/.claude/skills/app-teardown
```

## Use

Start Claude Code in your project and ask for what you want, for example "do a teardown of my app". Claude loads the matching skill from its description. You can also call a skill by name, like `/app-teardown`.

## How skills are written

Each skill:

- lives in its own folder, named after the skill, with a `SKILL.md` inside
- starts with frontmatter giving its `name` and a `description` that says when to use it
- breaks the work into numbered steps, each ending with a **Done when** line the agent checks before moving on
- says what it will and won't touch, and where its output goes

## Contributing

Ideas, fixes and new skills are welcome. Open an issue to suggest a skill, or a pull request that adds a new folder following the pattern above.

## License

[MIT](LICENSE)
