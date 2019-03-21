## ETCDとは  
分散KVSの一つ似たものとしてConsulがある  
keyとvuleを分散して保存することができる.  
kubernetesのシステムの状態を持っているそうな  

## Consulとetcdの違い
最近までconsulとetcdを競合のツールだと考えていたがどうやら違う  
純粋にkvsはetcdを指すのであろう.consulはサービスディスカバリ用のミドルウェアだ  
もちろんetcdもkvsを使用するdnsなどと組み合わせればサービスディカバリが可能だし  
coonsulもkvsとして使うことができる  

## dockerのoverlay network
flannelとetcdを使ってマルチホスト間でのdockerを使うことができる  
flannelで仮想ネットワークvxlanを作ってdocker runするときに付与されるIPをetcdに流して  
複数のホストでipを共有することができる

## etcdのdocker-composeを用意する
```docker-compose.yaml
version: "3"
services:
  etcd:
    image: gcr.io/etcd-development/etcd:latest
    ports:
      - 2379:2379
      - 2380:2380
    command: >
      /bin/sh -c "/usr/local/bin/etcd \
        --name s1 \
        --listen-client-urls http://0.0.0.0:2379 \
        --advertise-client-urls http://0.0.0.0:2379 \
        --listen-peer-urls http://0.0.0.0:2380 \
        --initial-advertise-peer-urls http://0.0.0.0:2380 \
        --initial-cluster s1=http://0.0.0.0:2380 \
        --initial-cluster-token tkn \
        --initial-cluster-state new"
```
