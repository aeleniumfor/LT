## kubernetesのpodに設定ファイルを入れたい場合
configmapで定義した記述をvolumeとしてマウントできるみたい

## GKEとEKSの違い
GKEはmasterとwokerどちらもマネジメントとして提供してくれている  
逆にEKSはmasterしか提供してくれず自分で立てる必要がある  
GKEにはβ版としてistioを入れてくれるがeksはそんなことはない  
EKSを選択する場合のingress controllrはaws-ingress-controllerがデファクトスタンダード

## IBM kubernetes IKSがかなり良さそう
kubernetesのfreeプランがある  
istioを実験的にいれてくれる

## aws kubernetesを構築する
eksを構築するのは大変.なのでeksctlを使うといいだろう  
コマンドを実行することでeksクラスタを組んでくれる
