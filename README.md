#テーブル設計

## users テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| email              | string  | null: false, unique: true |
| encrypted_password | string  | null: false               |
| nickname           | string  | null: false               |
| name               | string  | null: false               |
| birthdate          | integer | null: false               | 

### Association

- has_many :items
- has_many :comments
- has_many :orders

## items テーブル

| Column                     | Type      | Options                        |
| -------------------------- | --------- | ------------------------------ |
| item_name                  | text      | null: false                    |
| price                      | integer   | null: false                    |
| category                   | string    | null: false                    |
| item_state                 | string    | null: false                    |
| delivery_charge_burden     | string    | null: false                    |
| regional_original_delivery | string    | null: false                    |
| delivery_date              | string    | null: false                    |
| user                       | reference | null: false, foreign_key: true |

### Association

- belongs_to :users
- has_many   :comments
- has_many   :orders

## comments テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| text      | text       | null: false                    |
| user      | references | null: false, foreign_key: true |
| item      | references | null: false, foreign_key: true |

### Association

- belongs_to :users
- belongs_to :items

## orders テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| item      | references | null: false, foreign_key: true |

### Association

- belongs_to :users
- belongs_to :comments
- has_one    :delivery_address

## delivery_address テーブル

| Column                      | Type      | Options                        |
| --------------------------- | --------- | ------------------------------ |
| postal_code                 | integer   | null: false                    |
| prefectures                 | string    | null: false                    |
| city                        | string    | null: false                    |
| block                       | text      | null: false                    |
| building_name               | text      | null: false                    |
| phone_number                | integer   | null: false                    |
| user                        | reference | null: false, foreign_key: true |
| order                       | reference | null: false, foreign_key: true |

### Association

- belongs_to :users
