# Infrastructure Inventory — 現行インフラ台帳

## 1. 基本情報

| 項目 | 内容 |
|---|---|
| クライアント | Nexus Solutions Inc. |
| 運用形態 | オンプレミス |
| 設置場所 | 東京オフィス内サーバールーム |
| 物理サーバー数 | 8台 |
| ハードウェア使用年数 | 約5年 |
| ITインフラ担当者 | 3名 |
| 顧客企業数 | 200社 |
| 利用ユーザー数 | 約5,000人 |
| サービス提供時間 | 24時間365日 |
| 主な利用時間帯 | 平日9:00〜18:00 |
| ピーク時間帯 | 平日10:00〜12:00 |
| 将来の事業計画 | 3年以内に顧客企業数を2倍にする |

## 2. サーバー構成

### 2.1 ハードウェアスペック

スペックはサーバー1台あたりの値。

| サーバー | 台数 | CPU | RAM | Storage |
|---|---:|---:|---:|---|
| Web | 2 | 4 cores | 16GB | 256GB SSD |
| Application | 2 | 8 cores | 32GB | 512GB SSD |
| Database | 1 | 8 cores | 32GB | 2TB SSD |
| File | 1 | 4 cores | 16GB | 4TB HDD |
| Backup | 1 | 4 cores | 16GB | 8TB HDD |
| Dev/Test | 1 | 8 cores | 32GB | 1TB SSD |
| **合計** | **8** | **48 cores** | **192GB** | **約16.5TB** |

### 2.2 リソース使用率

| サーバー | 平均CPU | ピークCPU | 平均RAM | ピークRAM |
|---|---:|---:|---:|---:|
| Web | 20% | 45% | 35% | 55% |
| Application | 40% | 75% | 50% | 80% |
| Database | 40% | 95% | 60% | 90% |
| File | 15% | 35% | 30% | 50% |
| Backup | 10% | 65% | 25% | 60% |
| Dev/Test | 15% | 50% | 30% | 65% |

### 2.3 冗長化状況

| サーバー | 構成 |
|---|---|
| Web | 2台・負荷分散あり |
| Application | 2台・負荷分散あり |
| Database | 単一サーバー |
| File | 単一サーバー |
| Backup | 単一サーバー |
| Dev/Test | 単一サーバー |

- 負荷分散の具体的な方式は未確認
- Auto Scalingは未導入
- Database、File、Backupに単一障害点が存在する

## 3. ストレージ構成

| 対象 | 総容量 | 使用容量 | 使用率 | 年間増加量 |
|---|---:|---:|---:|---:|
| Database | 2TB | 800GB | 40% | 200GB |
| File | 4TB | 2.4TB | 60% | 600GB |
| Backup | 8TB | 5.6TB | 70% | 1.2TB |
| Dev/Test | 1TB | 300GB | 30% | 50GB |

- 確認済みの年間データ増加量：合計2.05TB
- Backup Serverの使用率が最も高い
- Web・Application Serverのストレージ使用量は未確認
- ディスクI/O性能は未調査

## 4. ネットワーク構成

### 4.1 ネットワーク情報

| 項目 | 内容 |
|---|---|
| インターネット回線 | 1Gbps |
| 内部ネットワーク | 1Gbps |
| 平均回線使用率 | 25% |
| ピーク回線使用率 | 65% |
| 月間Inbound Traffic | 2TB |
| 月間Outbound Traffic | 4TB |
| インターネット回線数 | 1 |
| Firewall | 1台 |
| Core Switch | 1台 |

### 4.2 ネットワーク分離

| ネットワーク | 主な用途 |
|---|---|
| DMZ | Web Server |
| Production | Application・Database |
| Management | 監視・バックアップ・管理 |
| Office | 社内PC・社内システム |

### 4.3 セキュリティ対策

- VLANによるネットワーク分離
- Firewallによる通信制限
- HTTPSによる通信の暗号化
- VPNによる管理者アクセス
- アクセスログの記録
- Databaseへの直接的なインターネットアクセスを制限

### 4.4 確認済みの課題

- インターネット回線の冗長化なし
- Firewallの冗長化なし
- Core Switchの冗長化なし
- 過去にFirewall障害による90分間のサービス停止が発生
- 単一拠点への依存
