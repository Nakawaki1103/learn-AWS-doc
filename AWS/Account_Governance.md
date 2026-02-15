# AWSアカウント管理・ガバナンス学習記録

## 学習概要
- AWS Organizationsによるマルチアカウント管理の構造
- Service CatalogとRAMによるリソース共有の違い
- IAM Identity Centerと認証・認可
- AWS Directory Serviceの種類と選び方

## AWS Organizationsとアカウント構造
- **IAMとの違い**:
    - IAMは「1つの家（アカウント）」の中の住人管理。
    - Organizationsは「マンション全体（組織）」の管理。
- **OU (Organizational Unit)**:
    - アカウントをグルーピングする「フォルダ」のようなもの（例：開発部OU、本番環境OU）。
    - OU単位でポリシー（SCP）を適用し、制限を一括管理できる。
- **メリット**: 請求の一元化、セキュリティ統制、環境の分離（開発環境でミスしても本番に影響しない）。

## Service Catalog vs RAM
- **Service Catalog**:
    - **「レシピ（設計図）」を配るサービス**。
    - 管理者が承認した構成（CloudFormationテンプレート）をカタログ化し、ユーザーはそこから選んで起動する。
    - 結果：ユーザーごとに「新しいリソース」が作成される。
    - 目的：構成の標準化、ガバナンス（勝手な設定で作らせない）。
- **RAM (Resource Access Manager)**:
    - **「実物（現物）」を貸すサービス**。
    - 自分が持っているリソース（VPCサブネットなど）を他アカウントに見せる。
    - 結果：リソースは1つのまま、みんなで共有して使う。
    - 目的：ネットワークなどの基盤共有。

## IAM Identity Center (旧 AWS SSO)
- **役割**: AWSアカウントへのシングルサインオン（SSO）管理サービス。
- **認証と認可の違い**:
    - **認証 (Authentication)**: 「あなたは誰ですか？」（本人確認）。パスワード入力など。
    - **認可 (Authorization)**: 「何をしていいですか？」（権限付与）。ポリシー適用など。
- **メリット**:
    - 1つのポータルにログインするだけで、複数のAWSアカウントにアクセスできる。
    - 外部IDプロバイダー（Google, Microsoftなど）と連携し、普段の社内アカウントでAWSにログインできる。

## AWS Directory Service
- **役割**: AWS上でActive Directory (AD) を利用するためのサービス。Windows環境のユーザー管理に必須。
- **主な3種類**:
    1.  **AWS Managed Microsoft AD**:
        - **本物**のWindows Server AD。
        - オンプレミスADと「信頼関係」を結べる。機能が一番豊富。企業の第一選択肢。
    2.  **AD Connector**:
        - **中継機（プロキシ）**。
        - AWS上にデータを持たず、認証リクエストをオンプレADに転送するだけ。
    3.  **Simple AD**:
        - **互換品**（Samba 4ベース）。
        - 安いが、オンプレ連携はできない。AWS内完結の小規模環境向け。

## 現時点での理解レベル
- Organizationsは「マンション管理組合」、IAMは「各部屋の家族」というスケール感の違いで理解。
- Service Catalogは「プレハブ住宅のカタログ（選べば建つ）」、RAMは「土地の共有（みんなで入る）」というイメージ。
- 認証＝本人確認、認可＝権限付与。IAM Identity Centerを使えばID管理を一元化できる。
- Directory Serviceは「Managed Microsoft AD」が本命で、あとは用途次第（中継か、簡易版か）。

## 理解に苦しんだところ

