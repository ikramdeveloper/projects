# Vonza — Live Streaming Feature

Vonza is a SaaS platform for creators and educators. I built the complete
live streaming module, handling everything from room creation to guest
access flows and automatic session recording.

<img src="https://projects-panel.s3.us-east-1.amazonaws.com/projects/images/0535ec16-d7f3-4890-bd64-92d3bff1d617-vonza-streaming-admin.png" />

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

  ## Link
  You can view project at <a href="https://vonza.com">Vonza</a>

  ## Attachments
  <img src="https://projects-panel.s3.us-east-1.amazonaws.com/projects/images/0bcfa1b2-d574-463e-99d4-e7cf10aaa1c8-vonza-streaming-create-stream.png" />
  <p>__Create New Stream__</p>

  <img src="https://projects-panel.s3.us-east-1.amazonaws.com/projects/images/599ef5b1-52a5-4299-aa36-c51af3c1a445-vonza-streaming-stream-screen.png" />
  <p>__Stream With Host__</p>
