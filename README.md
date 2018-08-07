# 概要

このリポジトリは、Unityの「サバイバルシューターチュートリアル」をWebVR化し、

アップロードする実験用のリポジトリである。8/6時点で最新のものである。

[gh-pagesリンク](https://akio-okumura.github.io/ShootingWebGL/)

# 問題点

MozillaのWebVRアセットをそのまま使えば、UnityコンテンツをWebVR化出来るが、

**既存のプロジェクトにカメラプレハブを置くだけでは上手く対応することが出来ない。**

この問題点を早急に解決することが必要とされている。

# 気付いた点

- ESCAPEによって、vrStateをトグルする状態にしてみた為気付いたことは、

　　VR化出来てない時は、MainCamera状態になっているということである。

　　つまりは、**VRモードボタンのクリックで、vrStateに遷移出来てない。**

___

- そして、**HMDのトラッキングが出来ていない**ので回らない。

　　これはvrStateをトグルして、ステレオカメラになってもトラッキング出来てないので

　　別の所に問題があると考えられる。

___

- シーンを開いてから、GAMEOVERになるまでなら、Escapeによるステレオ化は上手く行くが、

　　ゲームオーバー後はMainCameraのままなので、シーン遷移辺りにこれは問題がありそう。

___

- HUD Canvasを非アクティブにしたら、ブラウザで上手く動かなくなった、初めてのパターン。

```
Please note that Unity WebGL is not currently supported on mobiles.

Press OK if you wish to cointinue anyway.
```

~~何でか、下のゴーグルアイコンも見えなくなったしよくわからない。~~

~~**UICanvas無効化コミット**で何かが起きている。~~

~~1. TemplateDataの出現、何故だ…？~~

## これは解決した

PlayerSettingの、WebGLTenplateがDefaultになってしまっていたので、WebVRに変更で解決。

# Shootingと、砂漠のWebGLの違い

- webvr.js -> 相違点は検出されませんでした。

- index.html -> 11,12行目のタイトル、descriptionがそれぞれで違う。

```
<title>Sunny Desert | Testagain</title>
<meta name="description" content="Complete interactive 3D scene demo made in Unity and exported to WebVR with the WebVR template of the Unity WebVR assets">
```
  -> 31行目の`window.gameInstance = UnityLoader.instantiate('gameContainer', 'Build/webVR.json', {`

    ここは、Build/"フォルダ名".jsonになるので関係ない。

- sw.js -> 相違点は検出されませんでした。

- Build内の、UnityLoader.js -> 相違点は検出されませんでした。

- 差異は、Build内の.unityweb4つと、.jsonにありました。

その為、この2つのプロジェクト間で生まれている差は、**Unityエディタで編集して解決可能。**

# Build実験

- WebVRShootingプロジェクト内の、WebVRシーンをビルド -> 出来ない

  これより、サバイバルシューターを入れる時に、**既に何かが壊れてる可能性**

- Testagainプロジェクト**(これはVR化が出来るプロジェクトです)**で、[Cubeのシーンを作成しビルド](https://github.com/akio-okumura/CubeRepository/tree/gh-pages)

 これはVR化出来た。

- 0806Testプロジェクト。Learnからサバイバルシューターを選び、プロジェクト保存。

  選んだ時に、**API Update Required**が出てくるので、**Go,Ahead!**した。

  その後に、MozillaのアセットをImportしてwebVRシーンをいつものように配置。

  そのままWebGLでビルド。

  **サバイバルシューターをインポート、Mozillaアセット入れてビルドしただけのやつ**

  (https://github.com/akio-okumura/0806Test/tree/gh-pages)

  ## VR化出来ません

___

## 実験結論

- シンプルにWebVRアセットをビルド -> **VR化可能**

- サバイバルシューターをインポートしてから、WebVRアセット -> VR化不可能

  - この原因は不明であるが、サバイバルシュータープロジェクトのビルド設定か奥の方で、WebVRを妨げるようなことが起きていると判断

- 自分でプロジェクトを作成、WebVRアセットをインポートしてビルド -> **VR化不可能**

  **何故だ！！！！**
