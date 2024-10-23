```mermaid

erDiagram
    CUSTOMER {
        int customer_id PK "顧客ID"
        string name "氏名"
        string kana_name "ふりがな"
        string gender "性別"
        string email "メールアドレス"
        string phone "電話番号"
        string address "住所"
        int member_type "会員種別"
        int points "保有PT"
        date join_date "入会日"
        date birth_date "誕生日"
    }

    EVENT {
        int event_id PK "イベントID"
        string title "イベント名"
        string subtitle "サブタイトル"
        string organizer_name "主催者名"
        string speaker_name "講師名"
        string speaker_intro "講師紹介文"
        string description "概要"
        string schedule "スケジュール"
        date event_date "開催日"
        time start_time "開始時間"
        time end_time "終了時間"
        int min_participants "最小催行人数"
        int max_participants "最大参加人数"
        float fee "参加費"
        text notes "自由記入欄"
        int participant_points "参加PT付与数"
    }

    IMAGE {
        int image_id PK "画像ID"
        int event_id FK "イベントID"
        string image_type "画像種別"
        string image_url "画像URL"
        text description "説明文"
    }

    PARTICIPATION_HISTORY {
        int history_id PK "履歴ID"
        int event_id FK "イベントID"
        int customer_id FK "顧客ID"
        string comment "参加者のコメント"
        int rating "評価 (1-5)"
        float total_payment "入金総額"
        float support_fee "運営サポート費"
        float final_payment "差し引き振込額"
        text cafe_feedback "cafeスタッフのフィードバック"
        string feedback_writer "記入者"
        text improvement "改善点"
        text positive_points "良かった点"
    }

    CRM {
        int crm_id PK "CRM ID"
        int customer_id FK "顧客ID"
        text inquiry_history "問い合わせ履歴"
        text participation_history "参加履歴"
        text survey_results "アンケート結果"
    }

    CUSTOMER ||--o{ PARTICIPATION_HISTORY : "参加"
    EVENT ||--o{ PARTICIPATION_HISTORY : "記録"
    CUSTOMER ||--o{ CRM : "管理"
    EVENT ||--o{ IMAGE : "関連する画像"
    CUSTOMER ||--o{ EVENT : "参加する"
