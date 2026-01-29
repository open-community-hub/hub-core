# Architecture (MVP)

## Goals
- Ship a usable MVP quickly without over-engineering
- "Hub-in-a-box" deployment via Docker Compose
- Strong privacy defaults for sensitive requests (e.g., help at home)
- Federation-ready data model, without implementing federation in MVP

## Stack (recommended)
- Web: SvelteKit + TypeScript
- API: Fastify + TypeScript
- DB: PostgreSQL
- ORM/Migrations: Prisma
- Validation: Zod (shared schemas in `packages/shared`)
- Deploy: Docker Compose

## Repo Layout
- `apps/web`: SvelteKit UI
- `apps/api`: Fastify API
- `packages/shared`: shared Zod schemas/types/constants
- `prisma`: Prisma schema + migrations
- `infra`: Docker Compose and deployment notes
- `docs`: spec, architecture, operational guide

## Core Concepts
### Hub
A hub is a single community/neighborhood deployment.

### Posts
Two post types in MVP:
- `Need`: A request for help (snow removal, small repairs, rides, etc.)
- `Opportunity`: A chance to help (food drive, cleanup day, tutoring event)

Future (not MVP):
- `Event`, `Class`, `Resource` (maker spaces)

### Privacy Defaults
- Posts show **approximate location** by default (neighborhood/cross-streets).
- Exact addresses are stored privately and revealed only after a volunteer is accepted.
- Messaging is limited to matched/accepted parties.

### Moderation
- Any user can flag posts/messages/users/orgs.
- Moderators can remove content, warn/suspend/ban users, and verify orgs.
- Moderation actions are logged.

## Federation Readiness (not implemented in MVP)
Schema includes:
- UUID ids
- `visibility` fields (default: `LocalOnly`)
- Optional external identifiers for future federation

