# 概要

このリポジトリは、Unityの「サバイバルシューターチュートリアル」をWebVR化し、

アップロードする実験用のリポジトリである。8/6時点で最新のものである。

# 問題点

MozillaのWebVRアセットをそのまま使えば、UnityコンテンツをWebVR化出来るが、

**既存のプロジェクトにカメラプレハブを置くだけでは上手く対応することが出来ない。**

この問題点を早急に解決することが必要とされている。

# 気付いた点

- ESCAPEによって、vrStateをトグルする状態にしてみた為気付いたことは、

　　VR化出来てない時は、MainCamera状態になっているということである。

　　つまりは、**VRモードボタンのクリックで、vrStateに遷移出来てない。**

- そして、**HMDのトラッキングが出来ていない**ので回らない。

　　これはvrStateをトグルして、ステレオカメラになってもトラッキング出来てないので

　　別の所に問題があると考えられる。
