# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

## usersテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|name_kana|string|null: false|
|nickname|string|null: false|
|sex|integer|null: false|
|birthday|integer|null: false|
|email|string|null: false|
|password|string|null: false|
|tel|integer|null: false|
|identification|string|null: false|
|card|string|null: false|
|image|string|null: false|
|point|integer|
|sales|integer|
|to_do|integer|
|certification|string|null: false|
### Association
- has_many :likes
- has_many: evaluations
- has_many: items
- has_many: dms
- has_many: commnets
- has_many: sns_credentials
- has_one :address


## addressesテーブル
|Column|Type|Options|
|------|----|-------|
|postal_code|integer|null: false|
|address|string|null: false|
|user_id|integer|null: false, foreign_key: true|
|type|integer|null: false|
### Association
- belongs_to :user, optional: true


## likesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|item_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :item



## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|comment|text|null: false|
|large_category|integer|null: false, foreign_key: true|
|middle_category|integer|null: false, foreign_key: true|
|small_category|integer|null: false, foreign_key: true|
|condition|integer|null: false|
|brand|integer|null: false|
|complete_day|integer|null: false|
|seller_id|integer|null: false, foreign_key: true|
|buyer_id|integer|null: false, foreign_key: true|
|size|integer|null: false|
|price|integer|null: false|
|arrival_date|integer|null: false|
|charge|integer|null: false|
|location|string|null: false|
|status|integer|null: false|
|delivery|integer|null: false|

### Association
- belongs_to:user
- has_many :likes
- has_many:dms
- has_many:item_images
- has_many:item_comments
- belongs_to :large_category
- belongs_to :middle_category
- belongs_to :small_category


## item_commentsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|item_id|integer|null: false, foreign_key: true|
|comment|text|null: false|
### Association
- belongs_to:user
- belongs_to:item


## item_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|integer|null: false, foreign_key: true|
|image|string|null: false|
### Association
- belongs_to:item


## large_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|integer|null: false|
|name|string|null: false|
### Association
- has_many :large_categories_middle_categories
- has_many :large_categories, through: :large_categories_middle_categories
- has_many :middle_categories
- has_many :items


## large_categories_middle_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|large_categories_id|integer|null: false, foreign_key: true|
|middle_categories_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :large_category
- belongs_to :middle_category


## middle_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|integer|null: false|
|name|string|null: false|
### Association
- has_many :middle_categories_small_categories
- has_many :middle_categories, through: :middle_categories_small_categories 
- has_many :small_categories
- has_many :large_categories_middle_categories
- has_many :large_categories, through: :large_categories_middle_categories 
- has_many :large_categories
- has_many :items


## middle_categories_small_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|middle_categories_id|integer|null: false, foreign_key: true|
|small_categories_id|integer|null: false, foreign_key: true|
### Association
- belongs_ to :middle_category
- belongs_ to :small_category


## small_categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|integer|null: false|
|name|string|null: false|
### Association
- has_many :middle_categories_small_categories
- has_many :middle_categories, through: :middle_categories_small_categories 
- has_many :middle_categories
- has_many :items


## dmsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|item_id|integer|null: false, foreign_key: true|
|comment|text|null: false|
### Association
- belongs_to:user
- belongs_to:item


## evaluationsテーブル
|Column|Type|Options|
|------|----|-------|
|judge|integer|null: false|
|comment|text|
|seller_id|integer|null: false, foreign_key: true|
|buyer_id|integer|null: false, foreign_key: true|
### Association
- belongs_to:user


## sns_credentialsテーブル
|Column|Type|Options|
|------|----|-------|
|uid|string|null: false|
|provider|string|null: false|
|token|string|null: false|
|user_id|integer|null: false, foreign_key: true|
### Association
- belongs_to :user