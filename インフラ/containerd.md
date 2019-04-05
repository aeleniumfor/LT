## containerdって何?
コンテナランタイムの一つでdockerの内部でつかわれているようだ

## containerdのinstall
containerdを動かすためには`libseccomp`が必要なので  
インストールする.ちなみに`libseccomp`はセキュリティ機構のようだ  

次にcontainerdをインストールしていく
```bash
$ wget https://storage.googleapis.com/cri-containerd-release/cri-containerd-1.2.5.linux-amd64.tar.gz
$ tar --no-overwrite-dir -C / -xzf cri-containerd-1.2.5.linux-amd64.tar.gz
$ systemctl start containerd
$ ctr version
Client:
  Version:  v1.2.5
  Revision: bb71b10fd8f58240ca47fbb579b9d1028eea7c84

Server:
  Version:  v1.2.5
  Revision: bb71b10fd8f58240ca47fbb579b9d1028eea7c84
```
インストール完了

## ansibleでinstallする場合
上でinstallした場合は必要ない  
ansibleでインストールできるものを用意した  
hosts.sampleを参考にipとkeyの設定を行えばcontainerdをインストールできる  
想定OSはCentos7だ

```bash
$ git clone https://github.com/aeleniumfor/ansible-code.git
$ sh ansible.sh
```
以上

## containerdでnginxを動かす
### nginxのimageをpullしてくる  
```bash
$ ctr i pull docker.io/library/nginx:latest
```
`$ ctr i ls`でimageがpullされたか確認できる

### nginxのコンテナを作る
```
$ ctr c create docker.io/library/nginx:latest nginx
```
`docker.io/library/nginx:latest`はさっきpullしてきたimageの名前  
そして`nginx`はIDになるので任意の文字を与えるといい  
コンテナが作成されたか確認する
```
$  ctr c ls
CONTAINER    IMAGE                             RUNTIME                           
nginx        docker.io/library/nginx:latest    io.containerd.runtime.v1.linux
```

### nginxコンテナを動かす
createしただけでは動かないのでスタートさせる  
```
$ ctr task start nginx

```
何もエラーが表示されていなければ動いているだろう

## containerdコンテナの後かたずけ
### 起動しているコンテナをすべてkillする
```bash
$ ctr t kill -s 9 $(ctr t ls -q)
```
### Killしたコンテナをdeleteする
```bash
$ ctr t delete $(ctr t ls -q)
```
### 作成したコンテナを一括削除
```bass
$ ctr c delete $(ctr c ls -q)
```
