# Jenkins Pipelines for Azure Kubernetes Services

## Jenkins サーバーの構築
### インストール
[Azure Marketplace イメージからのインストール](https://docs.microsoft.com/ja-jp/azure/jenkins/install-solution-template-quickstart)

Docker
```shell-session
$ sudo apt install docker.io
```
kubectl
```shell-session
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$ sudo mv ./kubectl /usr/local/bin/kubectl
```

### 接続
```shell-session
$ ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@nvx-jenkins.eastus.cloudapp.azure.com
```

## Jenkins パイプラインの組み込み
### 利用する Jenkins Plugin
- [Kubernetes Continuous Deploy Plugin](https://github.com/jenkinsci/kubernetes-cd-plugin)

Azure Marketplace イメージからのインストールしているため、デフォルトでインストール済み。

### AKS に接続する kubeconfig
Jenkins の認証情報に kubeconfig を追加します。

- 種類：Kuberntes Configuration(kubeconfig) 
- kubeconfig：Enter directly

## Jenkins パイプラインを利用したデプロイ
Jenkins のプロジェクトに Jenkinsfile を配置します。  
Jenkinsfile のパラメータを変更し、Jenkins パイプラインを実行します。
| パラメータ | パラメータ値 |
----|---- 
| DOCKER_IMAGE_TAG | デプロイするコンテナイメージのタグ（バージョン） |
| NAMESPACE | デプロイ先となる顧客の Kubernetes Namespace |

## Jenkins パイプラインを利用した Blue / Green デプロイ
### Blue デプロイ
Jenkins のプロジェクトに Jenkinsfile を配置します。  
Jenkinsfile のパラメータを変更し、Jenkins パイプラインを実行します。
| 環境変数 | 設定値 |
----|---- 
| NAMESPACE | デプロイ先となる顧客の Kubernetes Namespace |
| VERSION | blue |
| DOCKER_IMAGE_TAG | デプロイするコンテナイメージのタグ（バージョン番号） |

### Green デプロイ
Jenkins のプロジェクトに blue-green ディレクトリ直下にある Jenkinsfile を配置します。  
新しいバージョンの Deployment のみデプロイしますが、古いバージョンの Deployment には影響を与えません。
| 環境変数 | 設定値 |
----|---- 
| NAMESPACE | デプロイ先となる顧客の Kubernetes Namespace |
| VERSION | green |
| DOCKER_IMAGE_TAG | デプロイするコンテナイメージのタグ（新しいバージョン番号） |

### Swap
Jenkins のプロジェクトに blue-green ディレクトリ直下にある Jenkinsfile を配置します。  
Service の Label Version を更新し、新しいバージョンの Deployment に切り替えます。
| 環境変数 | 設定値 |
----|---- 
| NAMESPACE | デプロイ先となる顧客の Kubernetes Namespace |
| VERSION | green |

