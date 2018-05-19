# データ領域(postgres)
rm -fr /tmp/data
mkdir /tmp/data
# ビルド(postgres)
cd postgres
docker build -t kube-postgres:1.0 .
cd ..
# デプロイ(postgres)
kubectl create -f postgres-deployment.yaml
kubectl create -f postgres-service.yaml
# ビルド(wildfly)
cd wildfly
docker build -t kube-wildfly:1.0 .
cd ..
# デプロイ(wildfly)
kubectl create -f wildfly-deployment.yaml
kubectl create -f wildfly-service.yaml
# 動作確認
curl http://localhost:30080/myapp/service/main/foo?id=1
