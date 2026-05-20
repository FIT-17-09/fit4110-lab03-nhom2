FIT4110 Lab03 — Submission Summary

This repository contains the lab deliverables and evidence for FIT4110 Lab 03 (Postman + Prism mock + Newman + CI).

Required files (present):
- contracts/iot-ingestion.openapi.yaml
- contracts/ai-vision.openapi.yaml
- postman/collections/FIT4110_lab03_iot_ingestion.postman_collection.json
- postman/environments/FIT4110_lab03_mock.postman_environment.json
- postman/environments/FIT4110_lab03_local.postman_environment.json
- mock-data/*.json
- reports/newman-report.xml
- reports/newman-report.html
- reports/contract-lint-report.txt
- checklists/reliability_checklist.md (filled)
- templates/test-case-matrix.csv (filled)
- templates/consumer-provider-handshake.md (filled)

How to reproduce locally

1. Install deps:

```bash
npm install
```

2. Start Prism mocks (in separate terminals):

```bash
npm run mock:iot    # runs on http://localhost:4010
npm run mock:vision # runs on http://localhost:4011
```

3. Wait for health endpoints:

```bash
npx wait-on http://localhost:4010/health http://localhost:4011/health --timeout 30000
```

4. Run Newman against mock environment:

```bash
npm run test:mock
# or
node node_modules/newman/bin/newman.js run postman/collections/FIT4110_lab03_iot_ingestion.postman_collection.json -e postman/environments/FIT4110_lab03_mock.postman_environment.json -r cli,htmlextra,junit --reporter-htmlextra-export reports/newman-report.html --reporter-junit-export reports/newman-report.xml
```

5. Spectral lint (contract lint):

```bash
node node_modules/@stoplight/spectral-cli/dist/index.js lint contracts/*.yaml --fail-severity error
# output also saved in reports/contract-lint-report.txt in CI
```

Notes and known limitations
- Auth-related tests are present but are skipped on the Prism mock (Prism does not enforce auth by default). Run `npm run test:local` against your real service to validate auth behavior.
- Latency/SLA tests are marked as local-only and must be run against the real service.
- Spectral produced 2 info warnings about missing contact in `info` object; these are documented in `reports/contract-lint-report.txt`.

Evidence
- Newman HTML/XML reports: `reports/newman-report.html`, `reports/newman-report.xml`
- Spectral lint: `reports/contract-lint-report.txt`
 - Spectral lint: `reports/contract-lint-report.txt`

Local run notes:

- I attempted `npm run test:local` against `http://localhost:8000` to validate auth and local-only tests. The run failed with `ECONNREFUSED` (service not available). The full Newman output is saved at `reports/newman-local-runlog.txt`.
- To complete the remaining local checks, start your service on port 8000 and re-run:

```bash
# in project root
npm run test:local
```
- Test-case matrix: `templates/test-case-matrix.csv`
- Consumer–provider handshake: `templates/consumer-provider-handshake.md`

CI
- GitHub Actions workflow: `.github/workflows/newman.yml` (runs Spectral lint, starts Prism mocks, waits for health, runs Newman, uploads reports)

If you want, I can:
- Create a Pull Request for these changes.
- Run `npm run test:local` (if you have a local service running on `http://localhost:8000`).
- Open a GitHub Actions run link (cannot create runs from here, but pushing to branch will trigger CI).

Prepared by GitHub Copilot assistant.
