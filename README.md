# Sora Unity SDK 3D audio サンプル

## デモムービー

https://user-images.githubusercontent.com/59855953/195092231-dba39773-72d3-4c9e-8511-bf72a2847a64.mp4

↑ ミュートを解除してから再生してください。

## 概要

Sora Unity SDK は 時雨堂様の[WebRTC SFU Sora](https://sora.shiguredo.jp/) の Unity クライアントアプリケーションを開発するためのライブラリです。<br>
本サンプル Sora Unity SDK 3D audio は、[Sora Unity SDK](https://github.com/shiguredo/sora-unity-sdk) および [Sora Unity SDK Samples](https://github.com/shiguredo/sora-unity-sdk-samples) をforkし、Unityの立体音響機能を利用するための修正を加えたものです。<br>
可能な限り差分が少なくなるように配慮しましたが、一部でオリジナルと互換性のない部分があります。<br>

___

## 構成

本サンプルは3つのgithubプロジェクトで構成されています。
1) [sora-unity-sdk-3daudio](https://github.com/imageflux-jp/sora-unity-sdk-3daudio) Unityプラグイン
2) [sora-unity-sdk-samples-3daudio](https://github.com/imageflux-jp/sora-unity-sdk-samples-3daudio) Unityプロジェクト
3) [sora-3daudio-voicesend](https://github.com/imageflux-jp/sora-3daudio-voicesend) 複数の音声データと座標送信スクリプト

___

## ライセンス

ライセンスはオリジナルに準じます。<br>
<br>
時雨堂様オリジナルのSora Unity SDKについては [README_original.md](https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/README_original.md) をご覧ください。<br>
時雨堂様オリジナルのSora Unity SDK Sampleについては [README_original.md](https://github.com/imageflux-jp/sora-unity-sdk-samples-3daudio/blob/3daudio/README_original.md) をご覧ください。<br>
<br>
本サンプルで追加したファイルのうち、[dummy_audio_device.cpp](https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/src/dummy_audio_device.cpp) および [dummy_audio_device.h](https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/src/dummy_audio_device.h) は、Unity Technologies様の[WebRTCプラグイン](https://github.com/Unity-Technologies/com.unity.webrtc)のコードを利用し、一部修正しています。
[DummyAudioDevice.cpp](https://github.com/Unity-Technologies/com.unity.webrtc/blob/main/Plugin~/WebRTCPlugin/DummyAudioDevice.cpp) <br>
[DummyAudioDevice.h](https://github.com/Unity-Technologies/com.unity.webrtc/blob/main/Plugin~/WebRTCPlugin/DummyAudioDevice.h) <br>
Unity Technologies様のWebRTCプラグインのライセンスについては[こちら](https://github.com/Unity-Technologies/com.unity.webrtc/blob/main/LICENSE.md)をご覧ください。 <br>
<br>
[sora-3daudio-voicesend](https://github.com/imageflux-jp/sora-3daudio-voicesend) のライセンスは [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) とします。<br>

___

## ビルドと実行方法

Windowsでのみビルドおよび動作確認をしています。<br>
バイナリの配布は予定していません。ご自身でビルドしてください。<br>

### (1) sora-unity-sdk-3daudio プロジェクトのビルド方法
```
git clone -b 3daudio https://github.com/imageflux-jp/sora-unity-sdk-3daudio
```
Windows 11 dev environment等を利用し、Visual Studio 2022をアンインストールし、Visual Studio 2019 Community Editionをインストールした状態で、x64 Native Tools Command Prompt for VS 2019を開き、下記のコマンドを実行します。
```
python3 run.py windows_x86_64
```

生成された下記の2ファイルを次章(2)で使用します。
* sora-unity-sdk-3daudio\Sora\Sora.cs
* sora-unity-sdk-3daudio\\_build\windows_x86_64\release\sora_unity_sdk\Release\SoraUnitySdk.dll

### (2) sora-unity-sdk-sample-3daudio プロジェクトの実行方法

オリジナルと同じくpythonスクリプトでインストールしますが、その後に前章(1)の生成ファイルで上書きを行います。
```
git clone -b 3daudio https://github.com/imageflux-jp/sora-unity-sdk-3daudio
cd sora-unity-sdk-samples-3daudio
python3 install.py
```

前章(1)のsora-unity-sdk-3daudio プロジェクトで生成された2つのファイル
* sora-unity-sdk-3daudio\Sora\Sora.cs
* sora-unity-sdk-3daudio\\_build\windows_x86_64\release\sora_unity_sdk\Release\SoraUnitySdk.dll

をそれぞれ
* sora-unity-sdk-samples-3daudio\SoraUnitySdkSamples\Assets\SoraUnitySdk\Sora.cs
* sora-unity-sdk-samples-3daudio\SoraUnitySdkSamples\Assets\Plugins\SoraUnitySdk\windows\x86_64\SoraUnitySdk.dll

に上書きコピーしてください。

* sora-unity-sdk-samples-3daudio\SoraUnitySdkSamples\Assets\Scenes\3daudio.unity

をダブルクリックしてUnity Editorで開き、Hierarchyの中のScriptオブジェクトをクリックして、ImageFlux Live Streamingの`ImageFlux_20200316.CreateMultistreamChannel` APIを使用して取得した、`Signaling URL` および `Channel ID`をフォームにペーストしてください。

RUNボタンを押すと、接続開始して次章(3)の接続を待機します。

### (3) sora-3daudio-voicesend プロジェクトの実行方法

[こちらのページ](https://imageflux-jp.github.io/sora-3daudio-voicesend/voicesend.html)から利用可能です。<br>
![スクリーンショット 2022-10-12 082719](https://user-images.githubusercontent.com/59855953/195266398-444a6c96-3c66-4ee1-a434-b832c0d45e80.jpg)
ImageFlux Live Streamingの`ImageFlux_20200316.CreateMultistreamChannel` APIを使用して取得した、`Signaling URL` および `Channel ID`をフォームにペーストしてください。<br>
ブラウザ画面上部の4つの色のついた四角の中の「入室」ボタンを押すと、WebRTC接続します。<br>
(2)のUnity側画面にキャラクターが現れ、3D音声が再生されます。<br>
![スクリーンショット 2022-10-12 082650](https://user-images.githubusercontent.com/59855953/195266410-31d69899-712d-47cd-a265-9f692df15a21.jpg)
ブラウザ画面下部の同色の丸いシェイプをマウスでドラッグすると、3D座標を計算し、DataChannelで送信します。<br>
画面最下部の茶色いキャラクターがUnityのMainCameraに相当します。<br>
キャラクターを近づけると、音が大きくなり、遠ざけると、小さくなります。<br>
キャラクターを左右のどちらかに寄せると、ステレオ音声の左右差が聞き取れます。<br>
音声データのドロップダウンを変更すると、キャラクターが話す音声が切り替えられます。<br>
「退室」ボタンを押すとWebRTCを切断し、キャラクターが消えます。<br>

___

## 主要な改良点の解説

オリジナルのSora Unity SDKでは、オーディオデータをミックスして、1つのAudioClipで再生しています。<br>
本サンプルでは接続ごとにオーディオデータをUnityスクリプトに渡し、それぞれが座標を持つAudioClipで再生しています。<br>

### (1) sora-unity-sdk-3daudio プロジェクトの主要な改良点

ミックス前の個別のオーディオデータを受信するのに特に重要なのは以下の3箇所です。
* https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/src/dummy_audio_device.cpp#L49-L51 <br>
* https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/src/dummy_audio_device.h#L34 <br>
* https://github.com/imageflux-jp/sora-unity-sdk-3daudio/blob/3daudio/src/sora.cpp#L871-L873 <br>

### (2) sora-unity-sdk-sample-3daudio プロジェクトの主要な改良点

git差分ではわかりにくい、Inspector上の修正点は下記です。<br>
- Scene/multi_recvonly.unityを開き、別名保存(3daudio.unity) 
- HierarchyのCanvasオブジェクト: enabled -> disable
- HierarchyのAudioSourceOutputオブジェクト: enabled -> disabled
- HierarchyのPersonPrefabオブジェクト: 追加してenabled -> disabled
- HierarchyのScriptオブジェクト:
    - Audio Base Content: PersonPrefabを指定
    - Signaling Url: 空 -> ImageFlux Live Streamingの`ImageFlux_20200316.CreateMultistreamChannel` APIで取得した値を入れる
    - Channel Id: 空 -> ImageFlux Live Streamingの`ImageFlux_20200316.CreateMultistreamChannel` APIで取得した値を入れる
    - Video: enabled -> disabled
    - Unity Audio Output: disabled -> enabled
    - Data Channel Signaling: disabled -> enabled
    - Data Channels +ボタンを押す
        - Label: 空 -> #position
        - Direction: Sendonly -> RecvonlyまたはSendrecv

Hierarchy上のPersonPrefabにはAudioSourceをアタッチしていません。立体音響を使用するため、下記の箇所でspecialBlendプロパティ、loopプロパティを指定しています。 <br>
https://github.com/imageflux-jp/sora-unity-sdk-samples-3daudio/blob/3daudio/SoraUnitySdkSamples/Assets/SoraSample.cs#L339-L341

___

## 本サンプルの修正方法

### (1) sora-unity-sdk-3daudio プロジェクトの修正方法

受信専用として作成しているため、Unity側からのマイク入力の処理をスキップしています。<br>
UnityScriptとc++側の関数や引数の変更がなければ、Sora.cs のコピーは以降不要です。生成された SoraUnitySdk.dll だけをコピーしてください。<br>
SoraUnitySdk.dllを上書きする際はUnity Editorを毎回終了する必要があります。<br>

### (2) sora-unity-sdk-sample-3daudio プロジェクトの修正方法

キャラクターを変更するには、HierarchyのPersonPrefab以下を差し替えてください。<br>

色の変更は下記の箇所で行っています。目以外の子オブジェクトを一括で同じ色にしています。 <br>
https://github.com/imageflux-jp/sora-unity-sdk-samples-3daudio/blob/3daudio/SoraUnitySdkSamples/Assets/SoraSample.cs#L393-L399 <br>

キャラクター座標はHierarychy上はカメラと独立していますが、サンプルを簡単にするために、カメラ座標からの相対距離で計算しています。回転を加える場合や、カメラも動かしたい場合に修正が必要です。 <br>
https://github.com/imageflux-jp/sora-unity-sdk-samples-3daudio/blob/3daudio/SoraUnitySdkSamples/Assets/SoraSample.cs#L400 <br>

### (3) sora-3daudio-voicesend プロジェクトの修正方法

cloneしてお好みのWebサーバ経由でvoicesend.htmlを表示してください。VSCodeのLive Previewでも可能です。
```
git clone https://github.com/imageflux-jp/sora-3daudio-voicesend
```

音声データは[tts.py](https://github.com/imageflux-jp/sora-3daudio-voicesend/blob/main/tts.py)で生成しています。 
Google Cloud の [Text-to-Speech API](https://cloud.google.com/text-to-speech/docs/create-audio-text-command-line?hl=ja)を使用しています。 
読み上げる文章の一部は[青空文庫](https://www.aozora.gr.jp/)を使用しています。 

___

## 免責・無保証
本サンプルは無保証です。本サンプルを引用した結果生じた損害等、当方は一切責任を負いません。
