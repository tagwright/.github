<!-- SPDX-License-Identifier: GPL-3.0-or-later -->
# Security

This is the default security policy for the tagwright organization. It applies to
any repository here that does not carry its own `SECURITY.md`. Where a repository
does carry one, that file is the authority for that tool and this one steps aside.
The per-tool policies go further than this default, because each tool has its own
threat model worth stating exactly, so read a tool's own `docs/SECURITY.md` when
you are working with that tool.

## Reporting a vulnerability

Report a suspected vulnerability through GitHub's private vulnerability reporting
on the affected repository: open its **Security** tab and choose **Report a
vulnerability**. That opens a private advisory visible only to the maintainer,
which keeps the report out of public issues while it is being worked.

Please do not open a public issue for a security problem, and please do not
disclose it publicly before a fix is out. Disclosure is coordinated: a fix is
prepared and released first, and you are kept in the loop on timing.

If you cannot use private reporting on a repository for some reason, open a normal
issue that says only that you have found a security problem and asks how to send
the details privately. Do not put the details in that issue.

## What to expect

A report opens a private advisory that only the maintainer can see. The problem is
triaged there, a fix is prepared, and public disclosure follows the fix rather
than preceding it. Credit is given to the reporter unless you ask otherwise.

## Scope

The tagwright tools drive proven backends rather than reimplementing them. A tool
hands work to restic, an OpenTelemetry Collector, Authentik, Inspektor Gadget, and
the like, so a vulnerability in one of those backends is reported to that project,
not here. What belongs here is a problem in a tagwright tool itself: how it reads
labels, resolves secrets, reaches a runtime socket, or drives its backend. Each
tool's own `docs/SECURITY.md` states its trust boundary in detail.
