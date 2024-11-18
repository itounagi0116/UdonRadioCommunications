# UdonRadioCommunication  
VRChat Udonワールド用の簡易的な無線通信システム  

![image](https://user-images.githubusercontent.com/2088693/219715229-396f0e71-921a-4e2e-814a-d814944c3fe8.png)  

---

## はじめに  
1. **VRChat Creator Companion** を使用して、UdonSharpを含むVRChatワールド用のUnityプロジェクトを作成します。  
2. Unityプロジェクトを開きます。  
3. メニューの「Window」→「Package Manager」を開きます。  
4. 「+」ボタンをクリックし、`Add package from git URL` を選択します。  
5. 以下のURLを入力し、「Add」ボタンをクリックします：  
   - 通常版: `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications`  
   - ベータ版: `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications#beta`  
6. 必要に応じて[オプション依存関係](#optional-dependencies)をインストールしてください。

---

## 使用方法  
- 必要な場所に `Transmitter` と `Receiver` を配置します。  
- プレイヤーの操作により、カスタムイベント `Activate` と `Deactivate` を呼び出し、変数 `frequency` を設定します。  
- シーンに1つだけ `UdonRadioCommunication` を追加します。  

`Transceiver` の使用方法など、詳しい使い方は `Demo.unity` シーンを開いて確認してください。

---

## オプション依存関係  
| 名前 | 説明 |  
| :-- | :-- |  
| [InariUdon](https://github.com/esnya/InariUdon.git) | **サンプルプレハブで必須** の `Interaction/TouchSwitch` や `Interaction/KeyboardInput` を使用します。 |
| [UdonToolkit](https://github.com/orels1/UdonToolkit/) | InariUdonを動作させるために必要です。|

---

## 実行時の負荷  
`Update` ループを使用しているUdonスクリプトは1つだけです。`Transmitters` の数を `Nt`、`Receivers` の数を `Nr`、`Players` の数を `Np` とすると、計算量は `O(Np(Nt+Nr))` となります。

---

## 設定  

### Transceiver  
| プロパティ名 | 説明 |  
| :-- | :-- |  
| Exclusive | 送信中は受信をオフにします。 |  

### Receiver  
| プロパティ名 | 説明 |  
| :-- | :-- |  
| Sync | チェックすると、近くにいる全員が無線を聞くことができます。チェックしない場合はローカルクライアントのみが聞けます。 |  

---

# SaccFlightとの統合  
SaccFlightAndVehicles向けの統合アドオンです。周波数の管理、受信の切り替え、Push to Talk用のDFUNCを提供します。  

![image](https://user-images.githubusercontent.com/2088693/219712019-99885e55-98cc-4578-8931-456da063de62.png)  

---

## インストール  
1. メニューの「Window」→「Package Manager」を開きます。  
2. 「+」ボタンをクリックし、`Add package from git URL` を選択します。  
3. 以下のURLを入力し、「Add」ボタンをクリックします：  
   - 通常版: `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications-sf`  
   - ベータ版: `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications-sf#beta`  

---

### 追加資料(整備中)
以下に、 **このスクリプトの機能** の簡単な説明を追加しています(LLMを用いて作成している為その点はご留意下さい)

| **スクリプト名**                           | **説明**                                                                 |
|-------------------------------------------|-------------------------------------------------------------------------|
| **DFUNC_URC_Frequency**                  | 無線の周波数を調整するためのスクリプト。                                 |
| **DFUNC_URC_PTT**                        | PTT (Push-To-Talk) 操作を制御するスクリプト。                            |
| **DFUNC_URC_RX**                         | 受信モードの制御を行うスクリプト。                                       |
| **Receiver**                             | 無線受信機の動作を管理。                                                |
| **Transceiver**                          | 送受信機の統合動作を管理するスクリプト。                                 |
| **Transmitter**                          | 無線送信機の動作を管理。                                                |
| **UdonRadioCommunication**               | 無線通信システム全体のコントロールを提供。                              |
| **DesktopOnly**                          | デスクトップモードでのみ動作するオブジェクトの管理。                     |
| **RaycastBlocker**                       | デスクトップモードでのレイキャストを無効化。                             |
| **TransceiverEnabledTrigger**            | トランシーバーの初期設定や有効化トリガーを制御。                         |
| **TransceiverPickupTrigger**             | トランシーバーをピックアップした際の動作を制御。                         |

