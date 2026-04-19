# Vonza — Affiliate Management System

A full affiliate management module built inside the Vonza SaaS platform,
giving admins complete control over affiliate relationships and giving
affiliates a clean self-serve interface for promotions.

## What I Built

**Admin side:**
- Onboard any user as an affiliate directly from the admin panel
- Assign specific products each affiliate is allowed to promote
- Real-time stats dashboard showing revenue, commissions, and refunds
  broken down by affiliate

**Affiliate side:**
- Login and view only the products assigned to them
- Generate and copy unique referral links per product
- Track their own performance metrics

## Architecture

Same stack as the broader Vonza platform: Next.js frontend on a Turborepo
monorepo, NestJS microservices with RabbitMQ messaging, MongoDB, and
GraphQL API. AWS Amplify (frontend) and AWS App Runner (backend).

## Highlights

- Referral link system built to be product-scoped — each link carries
  affiliate ID and product context for accurate attribution
- Permissions model ensures affiliates only see and promote products
  explicitly assigned to them by an admin
- Stats aggregation pipeline handles revenue, commission calculations,
  and refund deductions in a single query layer
- Microservices boundary keeps affiliate tracking isolated from the
  core product and billing services
