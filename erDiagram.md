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
        timestamp updated_at
        bigint answerd_times "回答された回数：このカラムは問題が表示されたときではなく、回答ボタンをクリックされたときに加算される"
    }

    answer_logs {
        bigint id PK

    }
    %% answer_logsを使用して、回答することができなかった問題で絞り込んで出題する。

````