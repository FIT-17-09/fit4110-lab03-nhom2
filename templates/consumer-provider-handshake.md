# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-20
- Provider team: team-iot
- Consumer team: team-camera
- Provider service: iot-ingestion
- Consumer service: camera

## Contract

- Contract file: `contracts/iot-ingestion.openapi.yaml`
- Mock base URL: `http://localhost:4010`
- Auth method: Bearer token (set in Postman environment `authToken`)
- Endpoint được test: `POST /readings`, `GET /readings/latest`

## Smoke test

### Request (examples)

POST /readings

Authorization: Bearer {{authToken}}
Content-Type: application/json

```json
{
	"device_id": "ESP32-LAB-A01",
	"metric": "temperature",
	"value": 31.5,
	"unit": "celsius",
	"timestamp": "2026-05-13T08:30:00+07:00"
}
```

### Expected response (happy path)

```json
{
	"reading_id": "<uuid>",
	"device_id": "ESP32-LAB-A01",
	"metric": "temperature",
	"value": 31.5,
	"unit": "celsius",
	"accepted": true
}
```

## Kết quả

- [x] Consumer gọi mock thành công. (Newman mock run passed)
- [x] Consumer parse được field cần dùng. (`reading_id`, `accepted` present)
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về. (ProblemDetails shape observed)
- [x] Có Newman report hoặc screenshot. (`reports/newman-report.html`, `reports/newman-report.xml`)

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| | | | |

## Xác nhận

- Provider representative: (name/email)
- Consumer representative: (name/email)
