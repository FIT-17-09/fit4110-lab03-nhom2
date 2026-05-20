# Reliability Checklist — FIT4110 Lab 03

Điền checklist này trước khi nộp Lab 03.

## 1. Functional tests

- [x] Có test cho endpoint health. (Passed)
- [x] Có test happy path cho endpoint chính. (Passed)
- [x] Có kiểm tra status code 2xx. (Passed)
- [x] Có kiểm tra field quan trọng trong response. (Passed)
- [x] Có ít nhất 1 test đọc dữ liệu danh sách hoặc chi tiết. (Passed)

## 2. Auth tests

- [x] Có test thiếu token. (Test present; skipped on mock — Prism does not enforce auth. See `reports/newman-report-mock.xml`)
- [x] Có test sai token hoặc token rỗng. (Test present; skipped on mock)
- [x] Endpoint public được khai báo rõ nếu không cần auth. (N/A for these endpoints)
- [ ] Test thể hiện đúng expected status 401/403. (Requires running against local service to verify)

## Local run status

- Attempted to run Newman against the real local service (`npm run test:local`) on `http://localhost:8000`.
- Result: Connection refused (ECONNREFUSED). See `reports/newman-local-runlog.txt` for the captured output.
- Recommendation: Start the local service on port 8000 and re-run `npm run test:local` to validate auth and latency checks.

## 3. Negative tests

- [x] Có test thiếu field bắt buộc. (Passed)
- [x] Có test sai kiểu dữ liệu. (Passed where applicable)
- [x] Có test sai enum hoặc giá trị ngoài miền. (Passed)
- [x] Lỗi trả về theo cùng một error model. (ProblemDetails shape present in mock responses)

## 4. Boundary tests

- [x] Có test min/max hoặc dữ liệu sát ngưỡng. (Passed: value 80 accepted, 81 rejected)
- [x] Có test limit/pagination nếu endpoint có danh sách. (Passed: limit above max rejected)
- [ ] Có test payload lớn hoặc metadata thiếu. (Optional — not included)
- [x] Có ghi chú kỳ vọng xử lý dữ liệu biên. (Documented in test-case-matrix)

## 5. Reliability tests cơ bản

- [ ] Có kiểm tra response time. (Skipped on mock — meaningful on local)
- [ ] Có mô tả timeout mong muốn. (Add if team requires SLA)
- [ ] Có test hoặc ghi chú retry/idempotency nếu phù hợp. (Optional)
- [x] Có consumer-side smoke test với ít nhất 1 mock của nhóm khác. (Passed: AI Vision mock detect)

## 6. Evidence

- [x] Collection export JSON. (`postman/collections/FIT4110_lab03_iot_ingestion.postman_collection.json`)
- [x] Environment mock export JSON. (`postman/environments/FIT4110_lab03_mock.postman_environment.json`)
- [x] Environment local export JSON. (`postman/environments/FIT4110_lab03_local.postman_environment.json`)
- [x] Newman report XML/HTML. (`reports/newman-report.xml`, `reports/newman-report.html`)
- [x] Test-case matrix đã điền. (`templates/test-case-matrix.csv`)
- [x] Biên bản handshake đã điền. (`templates/consumer-provider-handshake.md`)

Notes:
- Running Newman against the real local service is recommended to verify auth and latency-related checks.
