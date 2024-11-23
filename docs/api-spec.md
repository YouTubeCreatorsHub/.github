# CreatorHub API 명세서

## 1. 콘텐츠 제작 도구 (Content Creation Tools)

### 1.1 썸네일 메이커 API
#### 썸네일 템플릿 관리
- **GET** `/thumbnails/templates`
- **GET** `/thumbnails/templates/{templateId}`
- **POST** `/thumbnails/templates`
- **PUT** `/thumbnails/templates/{templateId}`
- **DELETE** `/thumbnails/templates/{templateId}`

#### 썸네일 생성/편집
- **POST** `/thumbnails/create`
```json
{
    "templateId": "uuid?",
    "elements": [{
        "type": "text|image|shape",
        "content": "string",
        "position": {"x": "number", "y": "number"},
        "style": {}
    }]
}
```
- **PUT** `/thumbnails/{thumbnailId}/edit`
- **GET** `/thumbnails/{thumbnailId}/export`

### 1.2 키워드 분석 API
#### 키워드 검색 및 분석
- **GET** `/keywords/analyze`
  - 쿼리: keyword, platform, language
- **GET** `/keywords/trending`
  - 쿼리: category, platform, timeRange
- **GET** `/keywords/suggestions`
  - 쿼리: keyword, limit

#### 키워드 트래킹
- **POST** `/keywords/tracking`
- **GET** `/keywords/tracking`
- **DELETE** `/keywords/tracking/{trackingId}`

### 1.3 AI 콘텐츠 지원 API
#### 브레인스토밍 지원
- **POST** `/ai/brainstorm`
```json
{
    "topic": "string",
    "contentType": "video|blog|short",
    "targetAudience": "string",
    "preferences": {}
}
```

#### 자동 자막 생성
- **POST** `/ai/subtitles/generate`
- **PUT** `/ai/subtitles/{subtitleId}/edit`
- **GET** `/ai/subtitles/{subtitleId}/export`

## 2. 커뮤니티 (Community)

### 2.1 포럼 API
#### 게시글 관리
- **GET** `/forum/posts`
- **POST** `/forum/posts`
- **PUT** `/forum/posts/{postId}`
- **DELETE** `/forum/posts/{postId}`

#### 댓글 관리
- **GET** `/forum/posts/{postId}/comments`
- **POST** `/forum/posts/{postId}/comments`
- **PUT** `/forum/comments/{commentId}`
- **DELETE** `/forum/comments/{commentId}`

### 2.2 협업 매칭 API
#### 매칭 시스템
- **POST** `/collaboration/matching`
```json
{
    "type": "project|mentoring|collab",
    "requirements": {
        "skills": ["string"],
        "category": "string",
        "duration": "string"
    }
}
```
- **GET** `/collaboration/matches`
- **PUT** `/collaboration/matches/{matchId}/status`

### 2.3 멘토링 API
#### 멘토링 프로그램
- **GET** `/mentoring/programs`
- **POST** `/mentoring/programs`
- **GET** `/mentoring/sessions`
- **POST** `/mentoring/sessions/{sessionId}/feedback`

## 3. 데이터 분석 (Analytics)

### 3.1 채널 분석 API
#### 종합 분석
- **GET** `/analytics/dashboard`
  - 쿼리: timeRange, metrics
- **GET** `/analytics/reports/custom`
  - 쿼리: metrics, dimensions, filters

#### 경쟁사 분석
- **GET** `/analytics/competitors`
- **POST** `/analytics/competitors/add`
- **GET** `/analytics/competitors/comparison`

### 3.2 AI 인사이트 API
- **GET** `/analytics/ai/insights`
- **GET** `/analytics/ai/recommendations`
- **GET** `/analytics/ai/predictions`

## 4. 수익화 (Monetization)

### 4.1 광고 매칭 API
- **GET** `/monetization/ads/opportunities`
- **POST** `/monetization/ads/proposals`
- **GET** `/monetization/ads/campaigns`

### 4.2 디지털 상품 API
#### 상품 관리
- **POST** `/store/products`
```json
{
    "type": "course|ebook|template|resource",
    "title": "string",
    "description": "string",
    "price": "number",
    "files": ["string"]
}
```
- **GET** `/store/products`
- **PUT** `/store/products/{productId}`
- **DELETE** `/store/products/{productId}`

#### 판매 관리
- **GET** `/store/sales`
- **GET** `/store/sales/analytics`
- **POST** `/store/sales/refund`

## 5. 리소스 센터 (Resource Center)

### 5.1 리소스 라이브러리 API
#### 음원 관리
- **GET** `/resources/music`
  - 쿼리: genre, mood, duration
- **GET** `/resources/sound-effects`
- **GET** `/resources/music/{musicId}/license`

#### 이미지/영상
- **GET** `/resources/images`
- **GET** `/resources/videos`
- **POST** `/resources/upload`
  - Content-Type: multipart/form-data

### 5.2 템플릿 API
- **GET** `/templates`
- **GET** `/templates/{templateId}/preview`
- **POST** `/templates/customize`

## 6. 알림/스케줄링 (Notifications & Scheduling)

### 6.1 콘텐츠 캘린더 API
- **GET** `/calendar/events`
- **POST** `/calendar/events`
- **PUT** `/calendar/events/{eventId}`
- **DELETE** `/calendar/events/{eventId}`

### 6.2 자동화 워크플로우 API
- **POST** `/automation/workflows`
```json
{
    "name": "string",
    "triggers": [{
        "type": "schedule|event",
        "condition": {}
    }],
    "actions": [{
        "type": "string",
        "params": {}
    }]
}
```
- **GET** `/automation/workflows`
- **PUT** `/automation/workflows/{workflowId}`
- **GET** `/automation/workflows/{workflowId}/history`

## 7. 교육 및 성장 (Education & Growth)

### 7.1 온라인 강좌 API
- **GET** `/education/courses`
- **GET** `/education/courses/{courseId}`
- **POST** `/education/courses/{courseId}/enroll`
- **GET** `/education/courses/{courseId}/progress`

### 7.2 스킬 개발 API
- **GET** `/education/skills/assessment`
- **POST** `/education/skills/track`
- **GET** `/education/skills/recommendations`

## 8. 크로스 플랫폼 관리 (Cross-Platform Management)

### 8.1 플랫폼 연동 API
- **POST** `/platforms/connect`
- **GET** `/platforms/accounts`
- **DELETE** `/platforms/accounts/{accountId}`

### 8.2 통합 대시보드 API
- **GET** `/platforms/dashboard`
- **GET** `/platforms/metrics/unified`
- **POST** `/platforms/post/schedule`

## 공통 응답 형식 및 에러 처리

### 성공 응답
```json
{
    "success": true,
    "data": {},
    "timestamp": "2024-02-20T09:00:00Z",
    "metadata": {
        "page": "number?",
        "totalPages": "number?",
        "totalItems": "number?"
    }
}
```

### 에러 응답
```json
{
    "success": false,
    "error": {
        "code": "ERROR_CODE",
        "message": "에러 메시지",
        "details": "상세 에러 정보"
    },
    "timestamp": "2024-02-20T09:00:00Z"
}
```

## 보안 및 권한 관리

1. 인증 방식
- JWT 기반 인증
- OAuth2.0 소셜 로그인 지원
- API 키 인증 (서버 간 통신용)

2. 권한 레벨
- PUBLIC: 인증 불필요
- USER: 기본 사용자 권한
- CREATOR: 크리에이터 권한
- ADMIN: 관리자 권한

3. 보안 요구사항
- 모든 API는 HTTPS 사용
- Rate Limiting 적용
- CORS 설정 필수
- 민감한 데이터 암호화

## 버전 관리
- URI에 버전 명시 (/v1, /v2)
- 하위 호환성 유지
- 변경 이력 문서화
