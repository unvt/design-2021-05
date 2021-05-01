# Name
国連ベクトルタイルツールキット

# Purpose
あらゆるプレイヤーによる、ベクトルタイルの生産、スタイル、ホスト、最適化を支援すること。
また、そのための技術や工夫の共有を促進すること。

# Background
2017年以降、国土地理院のウェブ地図技術を
[国連地理空間情報課](https://www.un.org/geospatial/)や
[国連グローバルサービスセンター](https://www.ungsc.org/)に共有し、
[国連オープン GIS イニシアティブ](http://unopengis.org/)を通じ、
技術をともに発展させていくことになった。

# Overview
## 1. 生産
ソースデータを
[GeoJSON Text Sequence (GeoJSONS)](https://tools.ietf.org/html/rfc8142)
に変換し、ベクトルタイル設計情報を注入して
[Tippecanoe](https://github.com/mapbox/tippecanoe) で
[ベクトルタイル](https://github.com/mapbox/vector-tile-spec)の
[MBTiles](https://github.com/mapbox/mbtiles-spec)
パッケージに変換する。

ソースデータが小規模なら、
[tile-join](https://github.com/mapbox/tippecanoe#tile-join)
を使って MBTiles パッケージをファイルシステムに展開する。

ソースデータが大規模なら、数 GB 程度のモジュールに分割して生産する。

### タイル設計者のプロダクト (Tile Designer's product)
ベクトルタイル設計情報。通常、標準入力から与えられる GeoJSONS に
[Tippecanoe 用の GeoJSON 拡張属性](https://github.com/mapbox/tippecanoe#geojson-extension)
を追加するなどの加工をして GeoJSONS で標準出力に出力する、Ruby や JavaScript で書かれた
スクリプト。

## 2. スタイル
ベクトルタイル設計情報に合わせて、
[Style Specifications](https://docs.mapbox.com/mapbox-gl-js/style-spec/) に準拠した
style.jsonを生成する。

通常、style.json は大規模で複雑になることから、
[Human-Optimized Config Object Notation (HOCON)](https://github.com/lightbend/config#using-hocon-the-json-superset)
を用いてレイヤごとにファイルを分割して整理する。

### スタイル設計者のプロダクト (Style Designer's product)
ベクトルタイルスタイル情報。通常、HOCON ファイル （*.conf） のセット。

## 3. ホスト
ベクトルタイルやスタイルファイルなどのプロダクトをウェブにホストする。

ソースデータが小規模なら、通常、[budo](https://github.com/mattdesl/budo) 
でローカルにホストし、ウェブ公開する際には
[GitHub Pages](https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages)
を用いる。

## 4. 最適化
[vt-optimizer](https://github.com/ibesora/vt-optimizer)
を使って、ズームレベルごとのベクトルタイルのサイズ分布を分析し、
ベクトルタイル設計情報を継続的に改善する。

# System Context Diagram
![](system-context-diagram.jpg)

# Supporting Features
## [equinox: UNVT installer for Raspberry Pi OS](https://github.com/unvt/equinox)

## [plow: Server-side image tile rendering PoC](https://github.com/hfu/plow)

# Related Projects
## [Adopt Geodata (optgeo) project](https://github.com/optgeo)
