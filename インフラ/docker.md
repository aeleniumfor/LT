## dockerのネットワークについて
vxlanを張ることができる,flannelを使うのが良さそう
vxlanと連携することでマルチホストができる
flannelとetcdを連携すると複数のホストでipを共有することができる host1,host2,host3の間でcontainerにアクセスできるようになる
dockerのネットワーク複雑

## docker buildについて
docker build時に環境変数を渡したいときはArgを使う

## dockerの内部について
containerdを使っているようだ

## dockerにipを振りたくない場合
`$ docker run --network none alpine`
