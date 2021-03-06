.. -*- rst -*-

.. highlightlang:: none

はじめに
========

geo_distanceによる距離算出に関係したテストについて説明します。

ディレクトリ階層について
========================

test/function/suite/select/function/geo_distance以下にデータファイル
(csv)から生成されたテストファイル(.test)が配置されます。

geo_distanceにて距離を算出する場合に東経180度、西経180、北緯90度、
南緯90度の矩形領域を考えたとします。

この場合、a)任意に決定した二点間で直接線を引いたものが最短距離として扱われる
場合と、b) 領域内における二点間の経度差が180度を越える場合のように終端の点を
経の連続性から同一点と平行移動して考えた点に対して線を引いたものが最短距離とな
る場合とがあります。

a)の場合のイメージ(xが任意の点,<->が最短距離)::

  |   x<->x   |

b)の場合のイメージ(xが任意の点,<->が最短距離)::

  |->x     x<-|

本テストでは便宜上 a)の場合をshortとし、b)の場合をlongとして扱います。

テストパターンの生成方法について
================================

test/function/tools/geo/以下にgeo_distanceのテストに関連した
ファイルが配置されています。

geo_distance.csv .test生成元となるデータファイル
generate-grntest-data.rb geo_distance.csvから.testを生成するスクリプト

テストパターンを生成するには以下のようにコマンドを実行します。::

    % ruby1.9.1 generate-grntest-data.rb -c geo_distance.csv

テストデータのフォーマットについて
==================================

テストデータ(geo_distance.csv)のフォーマットはカンマ区切りのCSVとなっています。

第1列: 始点経度(度数表記)
第2列: 始点緯度(度数表記)
第3列: 終点経度(度数表記)
第4列: 終点緯度(度数表記)
第5列: 始点経度(ミリ秒表記)
第6列: 始点緯度(ミリ秒表記)
第7列: 終点経度(ミリ秒表記)
第8列: 終点緯度(ミリ秒表記)
第9列: 期待されるgeo_distanceの算出結果(メートル)
第10列: テストファイル名(.test)

テストパターンの追加削除等はgeo_distance.csvに対して行います。
期待される結果を固定したい場合には、上記第9列に値を指定します。







