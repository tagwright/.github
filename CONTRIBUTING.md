<!-- SPDX-License-Identifier: GPL-3.0-or-later -->
# Contributing

This is the default contributing guide for the tagwright organization. It applies
to any repository here that does not carry its own `CONTRIBUTING.md`. A repository
with its own guide overrides this one.

The suite is a set of small, single-purpose tools, and each lives in its own
repository. Work happens in the repository of the tool you are changing, not
across the whole org at once.

## Before you write code

Open an issue first for anything beyond a small fix. A bug report or a feature
request is the place to agree on the shape of a change before either of us spends
time on it. For a typo, an obvious bug, or a docs fix, a pull request on its own is
fine.

Each tool has a scope it means to keep. The whole point of the suite is that a tool
drives a proven backend rather than reimplementing it, so a change that reaches for
reimplementing the backend, or that widens a tool past what it is for, is likely to
be turned down no matter how clean the code is. The tool's README says what it is
for. Start there.

## Making a change

- Keep every source file's `SPDX-License-Identifier: GPL-3.0-or-later` header. New
  files need one too.
- Run the tests and make them pass. The tools gate their tests in CI, and each
  repository's `docs/TESTING.md` says what the coverage is and how to run it
  locally. A change that adds behavior adds the test that proves it.
- Match the style already in the repository rather than reformatting around your
  change. Commit messages are plain and descriptive and say whether the change
  preserves behavior or changes it.
- Keep pull requests focused. One change per pull request is easier to review and
  easier to revert if it needs to be.

## License of your contribution

The tagwright tools are licensed GPL-3.0-or-later, and a contribution is accepted
under that same license. By opening a pull request you are offering your change
under it. There is no separate contributor agreement to sign.

## Reporting a security problem

Do not use issues or pull requests for a vulnerability. Report it privately through
the affected repository's Security tab, as [SECURITY.md](SECURITY.md) describes.
