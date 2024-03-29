# WebRTC学習の記録

## 概要
**WebRTC**(Web Real-Time Communication)は、ウェブブラウザ間でのリアルタイムのオーディオ、ビデオ、データ通信を可能にする技術。
外部プラグインやソフトウェアを必要とせず、ブラウザだけで直接通信が行える。

この技術は例えば、オンラインゲームでの通話や、Google Meet、Discordなどで使われている。


## 基本知識
## NAT(Network Address Translation)

https://www.youtube.com/watch?v=jCaITiLbew4

**目的**

NATは、多くの家庭や企業のルーターで使われる技術。その主な目的は、プライベートなローカルネットワーク内の複数のデバイスが、1つの公共IPアドレスを共有してインターネットにアクセスすることを可能にすること。

<br>

**機能**

例えば、家庭内に複数のデバイス（スマートフォン、パソコンなど）がある場合、それぞれが独自のプライベートIPアドレスを持つ。NATを使用するルーターは、これらのプライベートIPアドレスからのトラフィックをインターネットに転送する際に、公共IPアドレスを使用して、外部のネットワークとの通信を仲介する。

<br>

**問題点**
外部からの直接的な接続（サーバーからクライアントへの直接接続）は困難。
つまり、AさんとBさんで通信したい場合、Aさん→サーバー→Aさん、Bさん→サーバー→Bさんの通信は可能だが、Bさん→サーバー→Aさん、Aさん→サーバー→Bさんはできない。
それを回避するためにSTUNサーバーがある。

## シグナリングと接続の確立
### シグナリングとは
シグナリングは、WebRTCでのコミュニケーションの最初のステップで、ピア(通信する端末)間の接続を確立するために必要。シグナリングを通じて、ピアは互いの存在を知り、通信を開始するための情報を交換する。

### シグナリングのプロセス

①ピア間の情報交換

シグナリングは、ピア間での通信を開始する前に、互いのネットワーク情報(IPアドレスなど)を交換することから始まる。これは、ピアが互いを「発見」し、通信を始めるために必要。

<br>

②セッションのパラメータ設定

ピアは、どの種類のメディア（ビデオ、オーディオ、その両方）を送受信するかを決定し、セッションのパラメータ（コーデック、解像度、帯域幅など）を設定する。

<br>

③オファー/アンサーの交換

シグナリングプロセスの核となる部分は、一方のピアから生成される「オファー」と、それに対するもう一方のピアの「アンサー」の交換。これらはSDP(Session Description Protocol)形式で行われ、通信のパラメータを定義する。

<br>

④ICE候補の交換

ICE(Interactive Connectivity Establishment)候補は、ピア間で最適な通信経路を見つけるためのネットワーク情報。これにより、NAT(Network Address Translation)やファイアウォールを越えた通信が可能になる。

<br>

⑤接続の確立

上記の情報交換が完了すると、ピア間で直接的な通信チャネルが確立され、メディアストリームの送受信が行われる。

補足
- SDP形式とは
- ICE候補とは
- メディアストリームとは　ストリーミング配信など聞き覚えがある
- NATとは

## NATトラバーサルとSTUN/TURNサーバー
### これらを学ぶ目的
### NATトラバーサル
多くのネットワーク環境ではNATが使用されており、これがP2P通信の障害となり得る。
NATトラバーサル技術を適用することで、リアルタイム通信を安定的に実現することが出来る。

### STUNサーバー
STUN(Session Traversal Utilities for NAT)サーバーは、NATの背後にあるデバイスの公開IPアドレスを特定するのに役立つ。これにより、ピアが互いについ維新可能な状態を確認し、接続を試みることが出来る。

両者のIPアドレスとポート番号を伝える。

### TURNサーバー
あるピアがNATやファイアウォールによって直接的な通信が不可能な場合、TURN(Traversal Using Relays around NAT)サーバーがリレーとして機能する。TURNサーバーを介してメディアストリームを転送することで、より厳しいネットワーク制約の中でも通信が可能になる。

## WebRTCのセキュリティ
## パフォーマンスと最適化
## P2P通信とSFU通信
