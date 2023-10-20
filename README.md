# アプリの概要

EPRecorderは誘発筋電図を記録するためのMATLABアプリです。
外部の刺激装置からのトリガによって、信号（誘発筋電位）を取り込みます。
そのほか、以下の機能を実装しています。

- 取り込んだ信号の保存
- グラフ化（波形プロット）
- 平均波形の描写

# 記録システムの構成

誘発筋電図を記録するためにはこのアプリの他に以下の装置が必要です。

- 刺激制御装置
- 信号増幅器（生体信号用）
- マルチファンクションデータ収集デバイス

# 開発およびテスト環境

システムの開発およびテストに用いた環境は以下の通りです。

## 刺激装置

- 製品名：簡易型刺激装置（SEN-5201MG）
- 販売元：株式会社ミユキ技研
- URL: https://www.miyuki-net.co.jp/

## 信号増幅器

- 製品名：高度増幅器（MEG-5100）
- 販売元：日本光電工業株式会社（2020年3月31日をもって販売終了）
- URL: https://www.miyuki-net.co.jp/jp/products_research/NKTransferProductGroup/

## マルチファンクションデータ収集デバイス

- 製品名：Multifunction I/O Device USB-6000
- 販売元：National Instruments Corp.
- URL: https://www.ni.com/ja-jp/support/model.usb-6000.html

## コンピュータ

- OS: Microsoft Windows 11 Pro
- MATLAB:
  - MATLAB R2022b
  - Data Acquisition Toolbox
  - Data Acquisition Toolbox Support Package for National Instruments NI-DAQmx Devices
 
# セットアップ

上記の開発およびテスト環境のセットアップ手順です。異なる環境で利用する場合は、セットアップも異なる場合があります。
その際は、利用する機器の手順に従ってください。

## インストール

### マルチファンクションデータ収集デバイス

NI社のUSB-6000を利用するためには以下の２つのドライバをインストールする必要があります。

- NI-DAQ mx (https://ni.com/r/downloaddaqmx)
- DAQExpress (https://ni.com/r/downloadexpress)

### MATLABおよびツールボックス

割愛。お使いの環境に合わせてインストールしてください。

### EPRecorder

GitHubのリポジトリから [ERP Recorder.mlappinstall](https://github.com/mokamotosan/EPRecorder/blob/master/build/EP%20Recorder.mlappinstall) をダウンロードしてファイルをクリックしてください。
MATLABを起動し、アプリタブに ERP Recorder があることを確認してください。

## 接続

### 刺激トリガ
簡易刺激装置の外部出力トリガを、マルチファンクションデータ収集デバイスのトリガチャンネルに接続

### 生体信号
好感度増幅器の出力を、マルチファンクションデータ収集デバイスのアナログ入力チャンネルに接続

## 使い方

MATLABを起動し、アプリタブから ERP Recorder を選び、アプリを起動します。

### 新規の被験者データを計測する

1. Mainウィンドウの「File/Data」メニューから「Create a new file (for a new participant)」を選んで、Dialogウィンドウを起動する。
2. Dialogウインドウに必要事項を入力し、「OK」ボタンを押して、Measウィンドウを起動する（新しいウィンドウの起動に少し時間がかかる場合があります）。
3. Measウィンドウの「Device」パネル（左）の「Device」から接続されているマルチファンクションデータ収集デバイスを選ぶ。
4. Measウィンドウの「Device」パネル（左）の「Channel」および「Rate」を確認する（通常はデフォルトのままでＯＫ）。
5. Measウィンドウの「Trigger」パネル（右）の「Trigger Channel」から接続されているマルチファンクションデータ収集デバイスのトリガチャンネルを選ぶ（USB-6000の場合は "Dev1/PFI1"）。
6. Measウィンドウの「Trigger」パネル（右）の「Trigger Level」および「Capture Duration (s)」を確認する（通常はデフォルトのままでＯＫ）。
7. Measウィンドウの「Device」パネル（左）の「Start」ボタンを押したあと、刺激装置で刺激を開始する（30秒以内）。

※同じ条件の試行を繰り返すときは、７を繰り返して記録を行う。

※異なる条件の試行を行う場合は、Measウィンドウを一旦閉じ、２から同様の操作を行う。

### データの保存

1. MeasウィンドウやDialogウィンドウが開いている場合は、いったん閉じる。
2. Mainウィンドウの「File/Data」メニューから「Save data」を選んで、データ保存ウィンドウを起動する。
3. 保存名（デフォルトは被験者ID）、保存先を選んでデータを保存する。

### 既存の被験者データを読み込み、新たにデータを計測・追加保存する

1. Mainウィンドウの「File/Data」メニューから「Load an existing data」を選んで、Dialogウィンドウを起動する。
2. Dialogウインドウに必要事項を入力し（被験者IDおよび年齢、性別は変更不可）、「OK」ボタンを押して、Measウィンドウを起動する（新しいウィンドウの起動に少し時間がかかる場合があります）。
3. Measウィンドウの「Device」パネル（左）の「Device」から接続されているマルチファンクションデータ収集デバイスを選ぶ。
4. Measウィンドウの「Device」パネル（左）の「Channel」および「Rate」を確認する（通常はデフォルトのままでＯＫ）。
5. Measウィンドウの「Trigger」パネル（右）の「Trigger Channel」から接続されているマルチファンクションデータ収集デバイスのトリガチャンネルを選ぶ（USB-6000の場合は "Dev1/PFI1"）。
6. Measウィンドウの「Trigger」パネル（右）の「Trigger Channel」の「Trigger Level」および「Capture Duration (s)」を確認する（通常はデフォルトのままでＯＫ）。
7. Measウィンドウの「Device」パネル（左）の「Start」ボタンを押したあと、刺激装置で刺激を開始する（30秒以内）。

※同じ条件の試行を繰り返すときは、７を繰り返して記録を行う。

※異なる条件の試行を行う場合は、Measウィンドウを一旦閉じ、２から同様の操作を行う。

### 波形グラフ

#### グラフの描写

データを記録または読み込んだ後、波形グラフは自動で描写されます。
ただし、サンプリング周波数（Sample Rate）とサンプリング期間（Sample Duration）が一意に定まらない場合は自動で描写されません。
その場合は、Mainウィンドウ右下の「Experiment Info」パネルで Sample Rate および Sample Duraion を選んでください。

#### 波形の絞り込み

特定の条件の波形のみ描写させたい場合は、「Experiment Info」パネルで条件を選んでください。
コントロールボタンを押しながらカーソルでクリックすると選択解除できます。

#### 平均波形

Plotタブに描写されている波形の平均波形を描写することができます。Mainウィンドウの「Analysis」メニューより「Averaged Waveform」を選んでください。

# このプロジェクトに関するヘルプ

- バグ報告やご要望などは [issue](https://github.com/mokamotosan/EPRecorder/issues) で受け付けています。
- ご質問は [GitHub Discussion](https://github.com/mokamotosan/EPRecorder/discussions) にどうぞ。GitHub Discussionの詳細は[ドキュメンテーション](https://docs.github.com/ja/discussions/collaborating-with-your-community-using-discussions/participating-in-a-discussion)をご覧ください。
