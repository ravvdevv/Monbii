# Architecture

This document describes the high-level system architecture of Monbii. Implementation details are not disclosed.

---

## Frontend

**React + Capacitor**

The UI is built with React and compiled to native mobile targets via Capacitor. This allows a single codebase to run on iOS and Android while maintaining access to native device APIs (notifications, haptics, storage).

The component structure is kept flat and feature-scoped. Screens map directly to user-facing concepts: habits, companion, battle.

---

## State Management

**Zustand**

Application state is managed with Zustand. Stores are kept narrow and purpose-specific — one for habits, one for companion state, one for user session. There is no shared global state beyond what's explicitly necessary.

State is persisted locally and synced with the backend on session load and key user actions.

---

## Backend / Cloud

**Supabase / Lovable Cloud**

Monbii uses Supabase for authentication, database, and real-time sync. User habit data, companion state, and progression records are stored server-side and associated with the authenticated user.

Lovable Cloud handles certain deployment and integration layers.

The backend is not exposed publicly. All client-server communication goes through authenticated API calls.

---

## Animation System

**Lottie**

Companion animations and UI transitions use Lottie. Animation files are pre-rendered and triggered by state changes in the companion system. This keeps animations performant and decoupled from rendering logic.

---

## Summary

```
User Device (iOS / Android)
        │
        ▼
React + Capacitor (Frontend)
        │
   Zustand (State)
        │
        ▼
Supabase / Lovable Cloud (Auth, DB, Sync)
```
