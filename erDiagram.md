```mermaid
erDiagram

    categories ||--|{ subcategories : "has"

    subcategories }|--|{ questions : "many-to-many"

    users {
        bigint id PK
        string name
        string password
    }

    %% ログインさえできればよいのでusersとcategoriesはひもづけない

    categories {
        bigint id PK
        string name 
        timestamp created_at
        timestamp deleted_at
    }

    %% カテゴリ名の変更、カテゴリの削除は管理者でも不可。名称の変更と削除はする必要がないため。

    %% ex)math.statistics, math.sequence
    %% ex)chemistry.organics
    %% ex)php
    
    subcategories {
        bigint id PK
        bigint category_id FK
        string name
    }

    %% ex)

    questions {
        bigint id PK
        bigint sub_category_id FK
        string problem
        string answer
        bigint answerd_times "回答された回数：このカラムは問題が表示されたときではなく、回答ボタンをクリックされたときに加算される"
        timestamp updated_at
    }

    subcategory_question {
        bigint subcategory_id
        bigint question_id
    }

    %% questinの編集、削除はadminのrole

    answer_logs {
        bigint id PK
        bigint question_id 
        boolean atterukadouka "正解か不正解（回答できなかったか）"
        timestamp created_at
    }
    %% answer_logsを使用して、回答することができなかった問題で絞り込んで出題する。
    %% answer_logsから苦手なsub_category, categoryを分析する。
    %% answer_logsから、直近1ヶ月以上前に回答してかつ、間違えた回数が3回以上のもので絞り込んで出題する。



````