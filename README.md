# FURIMA DB設計

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|family_name|string	null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birth_year|string|null: false|
|birth_month|string|null: false|
|birth_day|string|null: false|
|password|string|null: false|
|email|string|null: false, unique: true|
### Association
- has_many :products
- has_many :orders

## productsテーブル
|Column|Type|Options|
|------|----|-------|
|category_id|references|null: false, foreign_key: true|
|shipping_id|references|null: false, foreign_key: true|
|brand_id|references|null: false, foreign_key: true|
|user_id|references|null: false, foreign_key: true|
|name|string|null: false|
|text|text|null: false|
|condition|integer|null: false|
|price|integer|null: false|
|trading_status|integer|null: false|
|completed_at|datetime||
### Association
- belongs_to :user
- belongs_to :categories
- belongs_to :brands
- has_one :shipping
- has_one :order
- has_many :product_images

## ordersテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|product_id|references|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :product

## product_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|product_id|references|null: false, foreign_key: true|
|image_url|string|null: false|
### Association
- belongs_to :product

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|path|text|null: false|
|name|string|null: false|
|ancestry|string||	
### Association
- has_many :brands
- has_many :products
- has_ancestry

## brandsテーブル
|Column|Type|Options|
|------|----|-------|
|category_id|references|null: false, FK: true|
|brand_id|references|null: false, FK: true|
|name|string|null: false|
### Association
- has_many :products
- belongs_to :categories

## delivery_addressテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|zip_code|integer|null: false|
|prefecture|string|null: false|
|city|string|null: false|
|address1|string|null: false|
|address2|string|
|telephone|string|unique: true|
### Association
- belongs_to :user

## shippingテーブル
|Column|Type|Options|
|------|----|-------|
|area|string|null: false|
|fee|integer|null: false|
|type|string|null: false|
|handling_time|integer|null: false|
### Association
- belongs_to :product