# Vonza — Live Streaming Feature

Vonza is a SaaS platform for creators and educators. I built the complete
live streaming module, handling everything from room creation to guest
access flows and automatic session recording.

## What I Built

- Admins can create three stream types: scheduled, instant, and personal rooms
- Shareable room links with optional password protection
- Email-based invite system with role-scoped access
- Auto-recording mode that starts recording as soon as a stream begins
- Manual in-session recording toggle for admins
- Guest join flow with access validation (link + password or email invite)

## Architecture

Frontend runs on a Turborepo monorepo with Next.js, Zustand for state,
Shadcn/Tailwind for UI, and Apollo Client for GraphQL. Backend uses a
NestJS microservices architecture with RabbitMQ for inter-service messaging
and MongoDB for persistence. 100ms handles the real-time video/audio layer.
Frontend deployed on AWS Amplify, backend on AWS App Runner.

## Highlights

- Integrated 100ms SDK for production-grade real-time streaming with
  minimal latency across participant counts
- Designed the access control model to support three distinct entry
  flows (public link, password-protected link, email invite) without
  creating separate room types
- Auto-recording triggers at stream start via a webhook-driven flow,
  with no manual intervention required from the admin
- Microservices boundary kept streaming logic isolated — failures in
  recording do not affect the live session
