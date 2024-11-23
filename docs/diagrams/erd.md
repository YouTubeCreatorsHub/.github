```mermaid
erDiagram
    USERS ||--o{ CREATOR_PROFILES : has
    USERS ||--o{ SOCIAL_ACCOUNTS : manages
    USERS ||--o{ CONTENTS : creates
    USERS ||--o{ NOTIFICATIONS : receives
    
    CREATOR_PROFILES ||--o{ ANALYTICS : tracks
    CREATOR_PROFILES ||--o{ EARNINGS : records
    CREATOR_PROFILES }o--o{ COLLABORATIONS : participates
    
    CONTENTS ||--o{ COMMENTS : has
    CONTENTS ||--o{ ANALYTICS : generates
    CONTENTS ||--o{ RESOURCES : uses
    
    RESOURCES ||--o{ RESOURCE_CATEGORIES : belongs_to
    
    COLLABORATIONS ||--o{ MESSAGES : contains
    
    ANALYTICS ||--o{ ANALYTICS_METRICS : contains

    USERS {
        UUID id PK
        string email
        string password_hash
        string name
        string phone
        datetime created_at
        datetime updated_at
        boolean is_active
        string role
    }

    CREATOR_PROFILES {
        UUID id PK
        UUID user_id FK
        string channel_name
        string description
        string profile_image
        string category
        jsonb social_links
        datetime created_at
        datetime updated_at
    }

    SOCIAL_ACCOUNTS {
        UUID id PK
        UUID user_id FK
        string platform
        string account_id
        jsonb credentials
        boolean is_connected
        datetime connected_at
    }

    CONTENTS {
        UUID id PK
        UUID creator_id FK
        string title
        string description
        string content_type
        string status
        jsonb metadata
        datetime published_at
        datetime created_at
        datetime updated_at
    }

    ANALYTICS {
        UUID id PK
        UUID content_id FK
        UUID creator_id FK
        datetime date
        jsonb metrics
        datetime created_at
    }

    ANALYTICS_METRICS {
        UUID id PK
        UUID analytics_id FK
        string metric_name
        float metric_value
        string metric_type
        datetime recorded_at
    }

    RESOURCES {
        UUID id PK
        string name
        string type
        string url
        string license_type
        jsonb metadata
        datetime created_at
        datetime updated_at
    }

    RESOURCE_CATEGORIES {
        UUID id PK
        string name
        string description
        datetime created_at
    }

    COLLABORATIONS {
        UUID id PK
        UUID creator1_id FK
        UUID creator2_id FK
        string status
        datetime start_date
        datetime end_date
        jsonb terms
    }

    MESSAGES {
        UUID id PK
        UUID collaboration_id FK
        UUID sender_id FK
        text content
        datetime sent_at
        boolean is_read
    }

    NOTIFICATIONS {
        UUID id PK
        UUID user_id FK
        string type
        string title
        text content
        boolean is_read
        datetime created_at
    }

    EARNINGS {
        UUID id PK
        UUID creator_id FK
        decimal amount
        string currency
        string source
        string status
        datetime earned_at
        datetime paid_at
    }


#1. 핵심 사용자 관리
- `USERS`: 기본 사용자 정보 관리
- `CREATOR_PROFILES`: 크리에이터 전용 프로필 정보
- `SOCIAL_ACCOUNTS`: 연동된 소셜 미디어 계정 관리

#2. 콘텐츠 관리
- `CONTENTS`: 크리에이터가 제작한 콘텐츠 관리
- `RESOURCES`: 콘텐츠 제작에 사용되는 리소스 관리 (음악, 이미지 등)
- `RESOURCE_CATEGORIES`: 리소스 분류 체계

#3. 분석 및 성과 측정
- `ANALYTICS`: 콘텐츠 및 채널 성과 데이터
- `ANALYTICS_METRICS`: 세부 분석 지표 저장
- `EARNINGS`: 수익 추적 및 관리

#4. 협업 및 커뮤니케이션
- `COLLABORATIONS`: 크리에이터 간 협업 관리
- `MESSAGES`: 협업 관련 메시지 관리
- `NOTIFICATIONS`: 시스템 알림 관리

#주요 특징:
1. UUID 사용: 보안 및 확장성 고려
2. Soft Delete: 데이터 복구 가능성 유지
3. 감사 추적: created_at, updated_at 필드 포함
4. JSON 지원: 유연한 메타데이터 저장 (PostgreSQL의 jsonb 타입 활용)



