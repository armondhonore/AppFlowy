# Nexlayer — AppFlowy

<!-- nexlayer:meta version=1 analyzed=2026-07-02T05:21:38Z repo=https://github.com/armondhonore/AppFlowy branch=nexlayer -->

> **For AI agents (Claude Code, Cursor, Gemini CLI, Copilot):**
> This file is the **project context** for this Nexlayer deployment — tech stack, env vars, secrets, live URL.
> For full platform detail (nexlayer.yaml schema, Dockerfile rules, CI/CD, task recipes) read **`nexlayer.skills`** in this repo.
>
> **Critical rules (full detail in `nexlayer.skills`):**
> - Inter-pod refs: `${podName:port}` only — never `localhost` or bare hostnames
> - Docker Hub images: prefix with `mirror.gcr.io/library/` — bare tags fail on the cluster
> - Secrets: set in the Nexlayer dashboard — never commit to `nexlayer.yaml` or Dockerfile
>
> **This file:** `agent-managed` sections update automatically. `user-editable` sections (Local Development Setup, Nexlayer Deployment Plan, Build Notes) are yours — preserved across re-analysis.

## Project Summary
<!-- nexlayer:section agent-managed=project_summary -->
AppFlowy is an open-source alternative to Notion, providing an AI-powered workspace for notes, kanban boards, and databases with a focus on data ownership.
<!-- nexlayer:end -->

## Technology Stack
<!-- nexlayer:section agent-managed=tech_stack -->
| Name | Kind | Version | Detected From |
|------|------|---------|---------------|
| Nginx | infra | alpine | Dockerfile |
| Flutter | framework | latest | README.md, frontend |
<!-- nexlayer:end -->

## Repository Structure
<!-- nexlayer:section agent-managed=structure_map -->
- frontend/ — Frontend application source code
- Dockerfile — Nginx configuration for serving static assets
- nexlayer.yaml — Platform configuration
<!-- nexlayer:end -->

## External Services Required
<!-- nexlayer:section agent-managed=external_deps -->
_No external services detected._
<!-- nexlayer:end -->

## Local Development Setup
<!-- nexlayer:section user-editable=local_setup -->
### Prerequisites

- Flutter SDK
- Dart SDK

### Steps

1. `git clone https://github.com/armondhonore/AppFlowy.git` — Clone the repository
2. `cd frontend && flutter pub get` — Install frontend dependencies
3. `flutter run` — Start the application

<!-- nexlayer:end -->

## Nexlayer Setup
<!-- nexlayer:section agent-managed=nexlayer_setup -->
### Pod Environment Variables

| Pod | Variable | Value | Kind |
|-----|----------|-------|------|
| `web` | `APPFLOWY_BASE_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai"` | plain |
| `web` | `APPFLOWY_GOTRUE_BASE_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"` | plain |
| `web` | `APPFLOWY_WS_BASE_URL` | `"wss://relaxed-weasel-appflowy.cloud.nexlayer.ai/ws"` | plain |
| `app` | `RUST_LOG` | `info` | plain |
| `app` | `APPFLOWY_BASE_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai"` | plain |
| `app` | `APPFLOWY_WEB_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai"` | plain |
| `app` | `APPFLOWY_DATABASE_URL` | `postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy` | inter-pod |
| `app` | `APPFLOWY_REDIS_URI` | `redis://redis.pod:6379` | plain |
| `app` | `APPFLOWY_GOTRUE_BASE_URL` | `"http://gotrue.pod:9999"` | plain |
| `app` | `APPFLOWY_GOTRUE_JWT_SECRET` | _(set via Nexlayer dashboard)_ | secret |
| `app` | `APPFLOWY_GOTRUE_JWT_EXP` | _(set via Nexlayer dashboard)_ | secret |
| `app` | `APPFLOWY_GOTRUE_ADMIN_EMAIL` | `"admin@example.com"` | plain |
| `app` | `APPFLOWY_GOTRUE_ADMIN_PASSWORD` | _(set via Nexlayer dashboard)_ | secret |
| `app` | `APPFLOWY_GOTRUE_MAILER_AUTOCONFIRM` | `"true"` | plain |
| `app` | `APPFLOWY_ACCESS_CONTROL` | `"false"` | plain |
| `app` | `APPFLOWY_S3_USE_MINIO` | `"true"` | plain |
| `app` | `APPFLOWY_S3_MINIO_URL` | `"http://minio.pod:9000"` | plain |
| `app` | `APPFLOWY_S3_ACCESS_KEY` | `minioadmin` | plain |
| `app` | `APPFLOWY_S3_SECRET_KEY` | _(set via Nexlayer dashboard)_ | secret |
| `app` | `APPFLOWY_S3_BUCKET` | `appflowy` | plain |
| `app` | `APPFLOWY_S3_REGION` | `us-east-1` | plain |
| `app` | `APPFLOWY_S3_CREATE_BUCKET` | `"true"` | plain |
| `gotrue` | `GOTRUE_SITE_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai"` | plain |
| `gotrue` | `GOTRUE_EXTERNAL_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"` | plain |
| `gotrue` | `GOTRUE_URI_ALLOW_LIST` | `"**"` | plain |
| `gotrue` | `GOTRUE_DISABLE_SIGNUP` | `"false"` | plain |
| `gotrue` | `GOTRUE_JWT_ADMIN_ROLES` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `GOTRUE_JWT_AUD` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `GOTRUE_JWT_DEFAULT_GROUP_NAME` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `GOTRUE_JWT_EXP` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `GOTRUE_JWT_SECRET` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `GOTRUE_LOG_LEVEL` | `"ERROR"` | plain |
| `gotrue` | `GOTRUE_OPERATOR_TOKEN` | _(set via Nexlayer dashboard)_ | secret |
| `gotrue` | `DATABASE_URL` | `"postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy"` | inter-pod |
| `gotrue` | `API_EXTERNAL_URL` | `"https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"` | plain |
| `gotrue` | `GOTRUE_MAILER_AUTOCONFIRM` | `"true"` | plain |
| `gotrue` | `GOTRUE_DB_DRIVER` | `postgres` | plain |
| `postgres` | `POSTGRES_DB` | `appflowy` | plain |
| `postgres` | `POSTGRES_USER` | `postgres` | plain |
| `postgres` | `POSTGRES_PASSWORD` | `"${POSTGRES_PASSWORD}"` | inter-pod |
| `appflowy-db` | `mountPath` | `/var/lib/postgresql` | plain |
| `appflowy-db` | `size` | `10Gi` | plain |
| `minio` | `MINIO_ROOT_USER` | `minioadmin` | plain |
| `minio` | `MINIO_ROOT_PASSWORD` | _(set via Nexlayer dashboard)_ | secret |
| `minio` | `MINIO_DEFAULT_BUCKETS` | `appflowy` | plain |

### Secrets Required

Set these in the Nexlayer dashboard before deploying:

- `APPFLOWY_GOTRUE_JWT_SECRET` (`app` pod)
- `APPFLOWY_GOTRUE_JWT_EXP` (`app` pod)
- `APPFLOWY_GOTRUE_ADMIN_PASSWORD` (`app` pod)
- `APPFLOWY_S3_SECRET_KEY` (`app` pod)
- `GOTRUE_JWT_ADMIN_ROLES` (`gotrue` pod)
- `GOTRUE_JWT_AUD` (`gotrue` pod)
- `GOTRUE_JWT_DEFAULT_GROUP_NAME` (`gotrue` pod)
- `GOTRUE_JWT_EXP` (`gotrue` pod)
- `GOTRUE_JWT_SECRET` (`gotrue` pod)
- `GOTRUE_OPERATOR_TOKEN` (`gotrue` pod)
- `MINIO_ROOT_PASSWORD` (`minio` pod)

### nexlayer.yaml

```yaml
application:
  name: appflowy
  pods:
  # Web frontend — serves the AppFlowy UI at "/". It calls the cloud API at /api
  # and gotrue at /gotrue (same origin, routed by path below).
  - name: web
    image: mirror.gcr.io/appflowyinc/appflowy_web:latest
    path: /
    servicePorts:
    - 80
    vars:
      APPFLOWY_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_GOTRUE_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      APPFLOWY_WS_BASE_URL: "wss://relaxed-weasel-appflowy.cloud.nexlayer.ai/ws"
  - name: app
    image: mirror.gcr.io/appflowyinc/appflowy_cloud:latest
    path: /api
    servicePorts:
    - 8000
    vars:
      RUST_LOG: info
      APPFLOWY_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_WEB_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_DATABASE_URL: postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy
      APPFLOWY_REDIS_URI: redis://redis.pod:6379
      APPFLOWY_GOTRUE_BASE_URL: "http://gotrue.pod:9999"
      APPFLOWY_GOTRUE_JWT_SECRET: "gotrue-jwt-secret-appflowy-32chars"
      APPFLOWY_GOTRUE_JWT_EXP: "7200"
      APPFLOWY_GOTRUE_ADMIN_EMAIL: "admin@example.com"
      APPFLOWY_GOTRUE_ADMIN_PASSWORD: "Admin1234!"
      APPFLOWY_GOTRUE_MAILER_AUTOCONFIRM: "true"
      APPFLOWY_ACCESS_CONTROL: "false"
      # appflowy_cloud needs object storage; use the bundled MinIO pod.
      APPFLOWY_S3_USE_MINIO: "true"
      APPFLOWY_S3_MINIO_URL: "http://minio.pod:9000"
      APPFLOWY_S3_ACCESS_KEY: minioadmin
      APPFLOWY_S3_SECRET_KEY: minioadmin
      APPFLOWY_S3_BUCKET: appflowy
      APPFLOWY_S3_REGION: us-east-1
      APPFLOWY_S3_CREATE_BUCKET: "true"
  - name: gotrue
    image: mirror.gcr.io/appflowyinc/gotrue:latest
    path: /gotrue
    servicePorts:
    - 9999
    vars:
      GOTRUE_SITE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      GOTRUE_EXTERNAL_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      GOTRUE_URI_ALLOW_LIST: "**"
      GOTRUE_DISABLE_SIGNUP: "false"
      GOTRUE_JWT_ADMIN_ROLES: "supabase_admin"
      GOTRUE_JWT_AUD: "authenticated"
      GOTRUE_JWT_DEFAULT_GROUP_NAME: "authenticated"
      GOTRUE_JWT_EXP: "7200"
      GOTRUE_JWT_SECRET: "gotrue-jwt-secret-appflowy-32chars"
      GOTRUE_LOG_LEVEL: "ERROR"
      GOTRUE_OPERATOR_TOKEN: "operator-token-appflowy"
      DATABASE_URL: "postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy"
      API_EXTERNAL_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      GOTRUE_MAILER_AUTOCONFIRM: "true"
      GOTRUE_DB_DRIVER: postgres
  - name: postgres
    # appflowy_cloud migrations require the pgvector extension ("vector" type).
    image: mirror.gcr.io/pgvector/pgvector:pg16
    servicePorts:
    - 5432
    vars:
      POSTGRES_DB: appflowy
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: "${POSTGRES_PASSWORD}"
    volumes:
    - name: appflowy-db
      mountPath: /var/lib/postgresql
      size: 10Gi
  - name: redis
    image: mirror.gcr.io/library/redis:7-alpine
    servicePorts:
    - 6379
  - name: minio
    # The platform deploy backend (userDeploy.js:728) runs args.match() on a pod's
    # command/args and 500s when it's a list, so we must NOT set command/args.
    # The bitnami minio image auto-runs `minio server /bitnami/minio/data` from its
    # entrypoint, configured entirely by env vars — no command override needed.
    image: mirror.gcr.io/bitnamilegacy/minio:latest
    servicePorts:
    - 9000
    vars:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
      MINIO_DEFAULT_BUCKETS: appflowy
    # No PVC: bitnami minio runs as UID 1001 and can't write to a root-owned PVC
    # mount (the platform has no fsGroup/securityContext support). The image's own
    # /bitnami/minio/data is owned by 1001 and writable. Object storage is therefore
    # ephemeral — fine for this test deploy; appflowy recreates the bucket on boot.
```

<!-- nexlayer:end -->

## Nexlayer Deployment Plan
<!-- nexlayer:section user-editable=deployment_plan -->
### Pod Topology

| Pod | Image | Port | Role |
|-----|-------|------|------|
| appflowy-web | mirror.gcr.io/library/nginx:alpine | 80 | web |

### Deployment notes

- The current branch configuration utilizes a static Nginx server to host the frontend assets.
- Single pod deployment as no backend services or databases are defined in the provided Dockerfile/root structure.

<!-- nexlayer:end -->

## Build Notes
<!-- nexlayer:section user-editable=build_notes -->
<!-- Add notes for future builds here — preserved across re-analysis -->
<!-- nexlayer:end -->

## Nexlayer Configuration
<!-- nexlayer:section agent-managed=nexlayer_config -->
**Last deployed:** 2026-07-02T05:27:57Z  
**Live URL:** https://relaxed-weasel-appflowy.cloud.nexlayer.ai  
**Runtime:**  · **Port:** auto-detected  
**Deploy branch:** nexlayer  

```yaml
application:
  name: appflowy
  pods:
  # Web frontend — serves the AppFlowy UI at "/". It calls the cloud API at /api
  # and gotrue at /gotrue (same origin, routed by path below).
  - name: web
    image: mirror.gcr.io/appflowyinc/appflowy_web:latest
    path: /
    servicePorts:
    - 80
    vars:
      APPFLOWY_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_GOTRUE_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      APPFLOWY_WS_BASE_URL: "wss://relaxed-weasel-appflowy.cloud.nexlayer.ai/ws"
  - name: app
    image: mirror.gcr.io/appflowyinc/appflowy_cloud:latest
    path: /api
    servicePorts:
    - 8000
    vars:
      RUST_LOG: info
      APPFLOWY_BASE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_WEB_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      APPFLOWY_DATABASE_URL: postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy
      APPFLOWY_REDIS_URI: redis://redis.pod:6379
      APPFLOWY_GOTRUE_BASE_URL: "http://gotrue.pod:9999"
      APPFLOWY_GOTRUE_JWT_SECRET: "gotrue-jwt-secret-appflowy-32chars"
      APPFLOWY_GOTRUE_JWT_EXP: "7200"
      APPFLOWY_GOTRUE_ADMIN_EMAIL: "admin@example.com"
      APPFLOWY_GOTRUE_ADMIN_PASSWORD: "Admin1234!"
      APPFLOWY_GOTRUE_MAILER_AUTOCONFIRM: "true"
      APPFLOWY_ACCESS_CONTROL: "false"
      # appflowy_cloud needs object storage; use the bundled MinIO pod.
      APPFLOWY_S3_USE_MINIO: "true"
      APPFLOWY_S3_MINIO_URL: "http://minio.pod:9000"
      APPFLOWY_S3_ACCESS_KEY: minioadmin
      APPFLOWY_S3_SECRET_KEY: minioadmin
      APPFLOWY_S3_BUCKET: appflowy
      APPFLOWY_S3_REGION: us-east-1
      APPFLOWY_S3_CREATE_BUCKET: "true"
  - name: gotrue
    image: mirror.gcr.io/appflowyinc/gotrue:latest
    path: /gotrue
    servicePorts:
    - 9999
    vars:
      GOTRUE_SITE_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai"
      GOTRUE_EXTERNAL_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      GOTRUE_URI_ALLOW_LIST: "**"
      GOTRUE_DISABLE_SIGNUP: "false"
      GOTRUE_JWT_ADMIN_ROLES: "supabase_admin"
      GOTRUE_JWT_AUD: "authenticated"
      GOTRUE_JWT_DEFAULT_GROUP_NAME: "authenticated"
      GOTRUE_JWT_EXP: "7200"
      GOTRUE_JWT_SECRET: "gotrue-jwt-secret-appflowy-32chars"
      GOTRUE_LOG_LEVEL: "ERROR"
      GOTRUE_OPERATOR_TOKEN: "operator-token-appflowy"
      DATABASE_URL: "postgres://postgres:${POSTGRES_PASSWORD}@postgres.pod:5432/appflowy"
      API_EXTERNAL_URL: "https://relaxed-weasel-appflowy.cloud.nexlayer.ai/gotrue"
      GOTRUE_MAILER_AUTOCONFIRM: "true"
      GOTRUE_DB_DRIVER: postgres
  - name: postgres
    # appflowy_cloud migrations require the pgvector extension ("vector" type).
    image: mirror.gcr.io/pgvector/pgvector:pg16
    servicePorts:
    - 5432
    vars:
      POSTGRES_DB: appflowy
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: "${POSTGRES_PASSWORD}"
    volumes:
    - name: appflowy-db
      mountPath: /var/lib/postgresql
      size: 10Gi
  - name: redis
    image: mirror.gcr.io/library/redis:7-alpine
    servicePorts:
    - 6379
  - name: minio
    # The platform deploy backend (userDeploy.js:728) runs args.match() on a pod's
    # command/args and 500s when it's a list, so we must NOT set command/args.
    # The bitnami minio image auto-runs `minio server /bitnami/minio/data` from its
    # entrypoint, configured entirely by env vars — no command override needed.
    image: mirror.gcr.io/bitnamilegacy/minio:latest
    servicePorts:
    - 9000
    vars:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: minioadmin
      MINIO_DEFAULT_BUCKETS: appflowy
    # No PVC: bitnami minio runs as UID 1001 and can't write to a root-owned PVC
    # mount (the platform has no fsGroup/securityContext support). The image's own
    # /bitnami/minio/data is owned by 1001 and writable. Object storage is therefore
    # ephemeral — fine for this test deploy; appflowy recreates the bucket on boot.
```
<!-- nexlayer:end -->

## Build History
<!-- nexlayer:section agent-managed=build_history -->
| Date | Status | Notes |
|------|--------|-------|
| 2026-07-02T05:21:38Z | analyzed | initial repo analysis |
| 2026-07-02T05:27:57Z | success | deployed https://relaxed-weasel-appflowy.cloud.nexlayer.ai |
<!-- nexlayer:end -->
