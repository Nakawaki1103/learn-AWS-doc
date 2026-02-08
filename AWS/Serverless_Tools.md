# AWSサーバーレス開発ツール学習記録

## 学習概要
- AWS SAMとAWS SARの違いと関係性

## AWS SAM (Serverless Application Model)
- **役割**: サーバーレスアプリケーションを「作る」ための開発フレームワーク。
- **特徴**:
    - CloudFormationの拡張版。
    - LambdaやAPI Gatewayなどの構成を、非常に短いコード（短縮記法）で記述できる「設計図」。
    - `sam init`, `sam build`, `sam deploy` などのコマンドで開発サイクルを回す。

## AWS SAR (Serverless Application Repository)
- **役割**: サーバーレスアプリケーションを「配る・探す」ためのリポジトリ。
- **特徴**:
    - App StoreやDocker Hubのような場所。
    - SAMで作られた便利なアプリが公開されており、自分の環境にすぐにデプロイできる。
    - 公開（Public）だけでなく、社内限定（Private）での共有も可能。

## 現時点での理解レベル
- SAMで「作って」、SARで「配る（または探す）」という関係性。
- SAMは「HTMLを書くためのMarkdown」のように、CloudFormationを簡単に書くためのツールというイメージ。

## 理解に苦しんだところ

