# Architecture overview

This document outlines the high-level architecture for the Exchange P2P marketplace MVP.

Components
- Frontend: Next.js + TypeScript
  - Public pages, user dashboard, P2P listing pages, trade/chat UI
  - Design system (TailwindCSS + custom theme), responsive, dark-first

- Backend API: NestJS + TypeScript (REST initially)
  - Auth service (JWT + sessions, 2FA)
  - Users service (profiles, KYC status, reputation)
  - P2P service (listings, offers, matches)
  - Escrow service (wallet integration, transactions, dispute flow)
  - Chat service (WebSocket / real-time)
  - Billing/Fees service

- Wallet service (isolated microservice)
  - RPC providers (Infura/Alchemy, or self-hosted nodes)
  - Hot wallet + cold wallet management + multisig orchestration
  - Transaction queue and monitoring

- Database
  - PostgreSQL for core data
  - Redis for cache, locks, and ephemeral states

- Background workers
  - BullMQ / RabbitMQ for async jobs: sending txns, notifications, reconciliation

- Infrastructure
  - Docker + Kubernetes for deployment
  - CI/CD: GitHub Actions
  - Secrets: Cloud KMS or HSM

Security & Compliance
- 2FA (TOTP) and session hardening
- Rate limiting, input validation, CSP, HSTS, secure cookies
- Audit logging for sensitive actions
- Plan for smart contract audits if on-chain escrow is used

MVP Scope
- User registration/login + 2FA
- Create and browse P2P listings
- Initiate a trade: funds go to escrow (platform-managed multisig for MVP)
- In-trade chat and document upload
- Confirm payment and release funds
- Dispute flow and admin arbitration panel

Next steps
1. Create project scaffold in a feature branch
2. Implement auth and user models
3. Implement P2P listing and basic UI
4. Implement escrow mock (local) and wallet service interfaces
5. Integrate real wallet operations and conduct security review
