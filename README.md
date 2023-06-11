# [Recruit Restaurant Visitor Forecasting](https://www.kaggle.com/competitions/recruit-restaurant-visitor-forecasting)
![image](https://github.com/takuya-tokumoto/kaggle_recruit_restaurant/assets/58675697/1eb3420e-5419-4e55-8f6f-4abd30f2a71e)

# コンペ概要
- 予約・来店データを使って、未来の日付の飲食店の総来店者数を予測する


# 評価方法
- RMSLE
  - ![image](https://github.com/takuya-tokumoto/kaggle_recruit_restaurant/assets/58675697/f487b9a5-e52f-4358-9025-eb4ee7567789)
  - `n` : 総来店数
  - `p_i` : 来店予測数
  - `a_i` : 来店数の実数

# 提出形式
- テストセット内の店舗と日付の組み合わせごとに、提出ファイルには id と visitors の2つの列が含まれている必要があります
- idは、air_store_idとvisit_dateをアンダースコアで連結することで形成される。ファイルにはヘッダーが含まれ、以下の形式である必要があります
```
id,visitors
air_00a91d42b08b08d9_2017-04-23,0  
air_00a91d42b08b08d9_2017-04-24,0  
air_00a91d42b08b08d9_2017-04-25,0  
etc.
```

# データセット
## 概要

このコンペでは、レストランの来客を中心とした時系列予測の問題が出題されます。データは、2つの別々のサイトから入手したものです：

- ホットペッパーグルメ（hpg）：Yelpに似ていて、レストランを検索し、オンラインで予約することができます。
- AirREGI / レストランボード（air）：Squareに似ていて、予約管理・レジシステムです。  
これらのサイトからの予約、訪問、およびその他の情報を使用して、指定された日付の将来のレストラン訪問者の合計を予測する必要があります。トレーニングデータは、2016年から2017年4月までの日付を対象としています。テストセットは、2017年の4月と5月の最終週をカバーしています。テストセットは、時間に基づいて分割され（公開フォールドが最初に来て、非公開フォールドが公開に続く）、エアレストランの選ばれたサブセットをカバーしています。テストセットは、"ゴールデンウィーク "と呼ばれる日本の祝日の週を意図的にまたいでいることに注意してください。

テストセットには、レストランが閉まっていて来客がない日がある。これらは採点において無視される。トレーニングセットでは、レストランが閉まっていた日は除外しています。

## File Descriptions
これは2つのシステムからのリレーショナルデータセットである。各ファイルの先頭には、出所を示すためにソース（air_またはhpg_のいずれか）が付けられています。各レストランは一意のair_store_idとhpg_store_idを持つ。すべてのレストランが両方のシステムでカバーされているわけではなく、また、予測しなければならないレストラン以外のデータも提供されていることに注意してください。レストランの非識別化を防ぐため、緯度と経度は正確ではありません。

### air_reserve.csv
このファイルには、航空システムで行われた予約が含まれている。reserve_datetimeは予約が作成された時刻を示し、visit_datetimeは訪問が行われる未来の時刻であることに注意してください。

- `air_store_id` - airシステム内のレストランのIDです。
- `visit_datetime` - 予約が作成された時刻です。
- `reserve_datetime` - 予約が行われた時刻です。
- `reserve_visitors` - その予約の訪問者の数です。

### hpg_reserve.csv
このファイルには、hpgシステムで行われた予約が含まれています。

- `hpg_store_id` - hpgシステム内のレストランのIDです。
- `visit_datetime` - 予約が行われた時刻です。
- `reserve_datetime` -予約が行われた時刻です。
- `reserve_visitors` - その予約の訪問者の数です。

### air_store_info.csv
このファイルには、一部のエア・レストランに関する情報が含まれています。カラム名と内容は自明である。

- `air_store_id`
- `air_genre_name`
- `air_area_name`
- `latitude`
- `longitude`  
注）緯度経度は、店舗が属するエリアの緯度経度です。

### hpg_store_info.csv
このファイルには、一部のhpgレストランに関する情報が含まれています。カラム名と内容は自明である。

- `hpg_store_id`
- `hpg_genre_name`
- `hpg_area_name`
- `latitude`
- `longitude`  
注）緯度経度は、店舗が属する地域の緯度経度です

### store_id_relation.csv
このファイルにより、airとhpgの両方のシステムを持つ厳選されたレストランに参加することができます。

- `hpg_store_id`
- `air_store_id`

### air_visit_data.csv
このファイルには、エアレストランの過去の来店データが含まれています。

- `air_store_id`
- `visit_date` - 日付
- `visitors` - その日のレストランへの来客数

### sample_submission.csv
このファイルは、正しいフォーマットで投稿を示し、予測しなければならない日数を含みます。

- `id` - air_store_idとvisit_dateをアンダースコアで連結してidを形成します。
- `visitors` - 店舗と日付の組み合わせに対して予測される訪問者の数です。

### date_info.csv
このファイルは、データセットに含まれる暦日に関する基本的な情報を提供します。

- `calendar_date`
- `day_of_week`
- `holiday_flg` - 日本の祝日情報

# 引用 
https://github.com/MaxHalford/kaggle-recruit-restaurant
