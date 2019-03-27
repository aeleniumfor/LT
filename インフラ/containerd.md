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

## containerdのコマンド
