# Melody API & Backend

Backend documentation and database assets for **Melody**, a mobile music catalog and player application.

> This repository contains backend documentation, database definitions, API specifications, security policies, and storage documentation. The backend platform selected for Melody is **Supabase**. This repository is not a separate Express.js server.

## Project Overview

Melody is an Android application built with Kotlin and Jetpack Compose. It provides user authentication, music catalog browsing and management, playlists, favorites, search, and audio playback.

The mobile application communicates with the backend through Supabase services:

- **Supabase Auth** — user authentication and session management.
- **Supabase REST API (PostgREST)** — data access and JSON responses.
- **PostgreSQL** — primary relational database.
- **Row Level Security (RLS)** — backend-enforced data access policies.
- **Supabase Storage** — catalog audio and artwork files.

The Android application follows the approved MVVM and Repository Pattern architecture. Public music metadata lookup is handled separately through the MusicBrainz API; MusicBrainz is not the source of Melody's application database or audio streaming.

## Repository Scope

This repository is intended to contain:

| Area | Purpose |
|---|---|
| `docs/` | Backend architecture and API specifications |
| `database/` | PostgreSQL schema, migrations, and RLS policies |
| `storage/` | Storage bucket and file-structure documentation |

The Android application source code belongs in the separate [Mobile Repository](https://github.com/Yuratama1/0136_MelodyApp).

## Planned Structure

```text
0136_API_MelodyApp/
├── README.md
├── docs/
│   ├── architecture.md
│   └── api-specification.md
├── database/
│   ├── schema.sql
│   ├── migrations/
│   └── policies/
│       └── rls.sql
├── storage/
│   └── storage-structure.md
└── .gitignore
```

Files and directories will be added as their corresponding tasks are prepared and reviewed. The planned structure does not mean that the database, policies, or Supabase project have already been deployed.

## Core Data Model

The approved initial data model contains nine tables:

1. `users`
2. `songs`
3. `artists`
4. `albums`
5. `genres`
6. `playlists`
7. `playlist_songs`
8. `favorites`
9. `play_history`

Detailed columns, constraints, relationships, deletion behavior, and authorization rules will be documented in the database schema and policy files.

## Security Principles

- Authorization must be enforced by the backend using RLS, not only by hiding UI elements.
- Public registration must not allow a user to assign themselves the Admin role.
- Users may access and manage only their own playlists, favorites, and play history.
- Admin catalog-management permissions do not automatically grant access to users' personal music data.
- Supabase Service Role keys and other privileged secrets must never be embedded in the Android application.
- Secrets and local environment files must not be committed to this repository.

## Development Status

**Current status: Repository initialized; backend implementation and Supabase deployment have not yet been verified.**

Backend assets will be added progressively through the approved Melody task breakdown. A task is considered complete only after its acceptance criteria and evidence have been reviewed.

## Related Repository

- [Melody Android Mobile Repository](https://github.com/Yuratama1/0136_MelodyApp)

## Technology

- Supabase Auth
- Supabase REST API (PostgREST)
- PostgreSQL
- Row Level Security (RLS)
- Supabase Storage
- MusicBrainz Public API (metadata lookup)

---

This README describes the approved project direction. Update the development status only when supported by repository changes and implementation evidence.
