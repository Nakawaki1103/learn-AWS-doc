# AWS Codeサービス学習記録

## 実施したこと
- GitHubを使ってCI/CD環境を構築する
- リポジトリを作成
- CodeBuildeの設定
- CodeDeployの設定
- CodeBuide、CodeDeployを実行
- Pipelineを使い、CI/CDを作成

## CI/CD全体の流れ
1. 開発者　　　　　　　　　：コードを修正してpush
2. CodePipeline　　　　　　：修正を検知
3. CodeBuilde                         ：ビルドしてデプロイできる形に固める
4. CodePipeline                        ：CodeDeployへ指示
5. CodeDeploy                         ：ファイルをEC2に持っていって配置、Webサーバーを再起動

## 設定する流れ
1. Code Buildeの成果物を格納するS3バケットを作成
	1. バケットのバージョニングは有効に
2. buildespec.ymlの作成
	1. アプリケーションの名前を入力
	2. S3バケットの名前を入力
3. CodeBuildeの設定
	1. プロジェクトを作成する
	2. ソースのプロバイダは「GitHub」
		1. アカウント認証を行い自分のアカウントと接続する
	3. アーティファクトを選択
		1. タイプを「s3」に、バケットを作成した名前に（おそらく矢印の向き先を設定している？）
	4. IAMロールを修正する
		1. 自動的に作成された？アプリケーション名のIAMロールにCodeDeployDeployerAccessをアタッチする。インスタンスに紐づける
4. Code Deployの設定
	1. Web EC2インスタンス用のIAMロールを作成し、アタッチ
		1. S3のFullaccess権限を付与（S3からデータを取ってくるため）
		2. インスタンスに紐づける（ELBでEC2への向き先が複数ある場合は全てに紐づける
	2. Web EC2インスタンスにCodeDeployエージェントをインストール
		1. sshでEC2インスタンスに接続、CodeDeployのコマンドでインストール←1つのEC2インスタンスでしかインストールしてない気がしてきた、、、、確認
	3. CodeDeploy用のIAMロールを作成
		1. Code Deployのポリシーを追加
	4. Code Deployの設定を行う
		1. アプリケーションを作成
			1. アプリケーション名をそのまま使用
		2. デプロイグループを作成
			1. サービスロールを割り当てる←ここも怪しい
			2. ロードバランサーのターゲットグループも選択


## AWS CodeBuilde
- 自動テストやビルドを実行してくれるサービス
- 使用するにはビルドの使用を決めるファイルを定義（buildspec.ymlを使用）
- 

## 現時点での理解レベル
- PMMでpushしたら開発環境が自動デプロイされているのはこれか、、

## 理解に苦しんだところ
### 全部（復習中）
- デプロイ失敗した、、、見直し中
	- `The overall deployment failed because too many individual instances failed deployment, too few healthy instances are available for deployment, or some instances in your deployment group are experiencing problems.`
	


