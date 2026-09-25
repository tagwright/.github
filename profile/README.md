# tagwright

Label-driven, config-as-code companion tools for Docker and Podman. A container declares one piece of its own infrastructure through labels. A tagwright tool watches the container socket, reads those labels, and drives a proven backend to make the declaration real, instead of reimplementing the backend itself.

This is the shape Traefik proved for reverse proxying and Homepage proved for dashboards. The container already describes itself, and the tool does the wiring. tagwright points that pattern at the parts that usually live in some separate system: backups, log routing, egress, secrets, monitoring, and SSO.

One rule governs all of it. Never rebuild the part that would lose someone's data. Ballast drives restic, it does not write a backup engine. Bilgeline generates OpenTelemetry Collector config, it does not ship a log pipeline. The trust lives in the backend, and tagwright knows it is the glue.

## The tools

Daemons that watch the socket and drive a backend:

- [aboard](https://github.com/tagwright/aboard): single sign-on for Authentik. Reads `aboard.*` labels and reconciles the application, provider, and policy bindings inside Authentik over its API.
- [airlock](https://github.com/tagwright/airlock): egress visibility. Drives Inspektor Gadget's eBPF tracing to watch what a container actually connects to, and alerts when that drifts from what its labels declared. It observes, it does not block.
- [autogatus](https://github.com/tagwright/autogatus): monitoring for Gatus. Docker-label service discovery, the way Traefik does routes. Label a container and autogatus turns those labels into Gatus config and writes it where Gatus hot-reloads from, so a service joins the dashboard when you label it and drops off when you remove it.
- [ballast](https://github.com/tagwright/ballast): backups. Drives restic to back up each labeled service into its own repository.
- [bathyscaphe](https://github.com/tagwright/bathyscaphe): egress enforcement. For a container that opts in, it blocks the connections that violate policy in the kernel before they are made.
- [beacon](https://github.com/tagwright/beacon): one governed alert path per host. Everything that would page a human passes through a single policy for deduplication, storm suppression, correlation, and channel routing before it is delivered.
- [berm](https://github.com/tagwright/berm): secrets injection. A daemon holds the age key, decrypts SOPS- and age-encrypted sources, and hands each container only the secrets it declared. The label names a secret, it never carries one.
- [bilgeline](https://github.com/tagwright/bilgeline): log routing. Generates OpenTelemetry Collector config from labels and drives a collector you run, so it holds no exporter credentials and reads no log byte itself.

Shared libraries the tools build on:

- [core](https://github.com/tagwright/core): a Go container-runtime abstraction over Docker and Podman. List, inspect, watch the socket, read compose labels, exec.
- [courier](https://github.com/tagwright/courier): a small Go library for sending notifications and pushing telemetry. beacon uses it to do the actual delivery.

## The names

A tool's first letter tells you what family it belongs to. An A-name extends a named external product: aboard is built around Authentik, airlock around Inspektor Gadget, autogatus around Gatus. A B-name is tagwright's own tool, named for a part of a ship rather than for the backend it drives. That is ballast, beacon, berm, bilgeline, and bathyscaphe. You can tell which kind a tool is before you read a word of its docs. (core and courier are the shared libraries, not tools in that family.)

## License and security

The suite tools are GPL-3.0, except autogatus, which is Apache-2.0. A company can run them, build on them, and ship them, and for the GPL tools cannot take a modified version closed and sell it back. Each repository carries its own LICENSE and its own SECURITY policy for reporting a vulnerability there. Copyright is held by Nate Calvert.
