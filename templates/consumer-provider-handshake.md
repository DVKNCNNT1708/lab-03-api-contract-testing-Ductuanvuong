# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-20
- Provider team: team-vision
- Consumer team: team-camera
- Provider service: AI Vision Detection API
- Consumer service: Camera Stream

## Contract

- Contract file: `contracts/team-vision.openapi.yaml`
- Mock base URL: `http://localhost:4010`
- Auth method: `Authorization: Bearer <token>`
- Endpoint được test: `POST /vision/detect`, `GET /vision/detections/{detectionId}`, `GET /vision/models/info`

## Smoke test

### Request

```http
POST /vision/detect
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
  "requestId": "REQ-CAM-20260512-0001",
  "cameraId": "CAM-ER-01",
  "capturedAt": "2026-05-12T08:00:00Z",
  "traceId": "TRACE-20260512-0001",
  "zoneId": "ER-ENTRANCE",
  "motionLevel": 0.92,
  "imageSource": {
    "sourceType": "IMAGE_URL",
    "url": "https://media.hospital.local/camera/CAM-ER-01/frame-1001.jpg"
  }
}
```

### Expected response

```json
{
  "detectionId": "DET-20260512-0001",
  "requestId": "REQ-CAM-20260512-0001",
  "traceId": "TRACE-20260512-0001",
  "status": "PROCESSING",
  "acceptedAt": "2026-05-12T08:00:01Z"
}
```

## Kết quả

- [x] Consumer gọi mock thành công.
- [x] Consumer parse được field cần dùng.
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về.
- [x] Có Newman report hoặc screenshot.

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| Detection endpoint path | `/detect` | `/vision/detect` | team-vision + team-camera |
| Detection response id field | `detection_id` | `detectionId` | team-vision + team-camera |

## Xác nhận

- Provider representative: Group B4 (team-vision)
- Consumer representative: team-camera delegate
