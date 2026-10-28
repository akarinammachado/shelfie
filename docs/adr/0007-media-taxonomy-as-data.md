# 0007. Media taxonomy as data

- **Status:** Accepted
- **Date:** 2026-10-28

## Context

The app covers many media types and will keep adding more. They group by how they're consumed: read, watch, listen. Progress means different things per type (episodes, chapters, pages, minutes). Some stories exist in several media (a book and its audiobook, a manga and its anime).

## Decision

- Media types are rows in a `media_types` table, each with a consumption mode (`read`, `watch`, `listen`), a default progress unit and a label.
- Progress is generic: `current`, nullable `total`, `unit`.
- The same story in different media is separate Works linked by a `work_relation`.
- Individual song plays are out of scope for library entries; albums are tracked as Works.

## Alternatives considered

- **Hardcoded enum:** every new type needs a migration and deploy.
- **One Work with multiple formats/editions:** more precise, more complex; can be introduced later.
- **Songs as library entries:** volumes far beyond other media would distort the model; a separate play-events table can come later.

## Consequences

- New media types are a data change.
- GraphQL exposes one implementing type per mode, split further only when fields truly diverge.
