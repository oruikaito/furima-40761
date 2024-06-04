#テーブル設計

## users テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| email              | string  | null: false, unique: true |
| encrypted_password | string  | null: false               |
| nickname           | string  | null: false               |
| family_name        | string  | null: false               |
| first_name         | string  | null: false               |
| family_name_kana   | string  | null: false               |
| first_name_kana    | string  | null: false               |
| birthdate          | date    | null: false               | 

### Association

- has_many :items
- has_many :comments
- has_many :orders

## items テーブル

| Column                     | Type       | Options                        |
| -------------------------- | ---------- | ------------------------------ |
| item_name                  | string     | null: false                    |
| item_description           | text       | null: false                    |
| category_id                | integer    | null: false                    |
| status_id                  | integer    | null: false                    |
| burden_id                  | integer    | null: false                    |
| prefecture_id              | integer    | null: false                    |
| day_id                     | integer    | null: false                    |
| price                      | integer    | null: false                    |
| user                       | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_many   :comments
- has_one    :order

## comments テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| text      | text       | null: false                    |
| user      | references | null: false, foreign_key: true |
| item      | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :item

## orders テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| user      | references | null: false, foreign_key: true |
| item      | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :item
- has_one    :delivery_address

## delivery_addresses テーブル

| Column                      | Type       | Options                        |
| --------------------------- | ---------- | ------------------------------ |
| postal_code                 | string     | null: false                    |
| prefecture_id               | integer    | null: false                    |
| city                        | string     | null: false                    |
| block                       | string     | null: false                    |
| building_name               | string     |                                |
| phone_number                | string     | null: false                    |
| order                       | references | null: false, foreign_key: true |

### Association

- belongs_to :order
