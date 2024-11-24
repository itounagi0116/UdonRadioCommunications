# UdonRadioCommunication (日本語)

![ライセンスバッジ](https://img.shields.io/badge/ライセンス-MIT-007EC6)

[補足](https://github.com/itounagi0116/UdonRadioCommunication/blob/master/%E8%A3%9C%E8%B6%B3.md)

VRChatのUdonワールド向けに設計された、簡易的な無線通信システムです。  

![無線通信システムのイメージ](https://user-images.githubusercontent.com/2088693/219715229-396f0e71-921a-4e2e-814a-d814944c3fe8.png)  

---

## **始め方**  

1. **VRChat Creator Companion**を使用して、UdonSharpを含むVRChatワールド用のUnityプロジェクトを作成します。  
2. Unityプロジェクトを開きます。  
3. メニューの **Window** → **Package Manager** を開きます。  
4. 「+」ボタンをクリックし、**`Add package from git URL`** を選択します。  
5. 以下のURLを入力して「Add」ボタンをクリックします。  
   - **安定版リリース**:  
     `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications`  
   - **ベータ版リリース**:  
     `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications#beta`  
6. 必要に応じて[オプションの依存関係](#optional-dependencies)をインストールしてください。  

---

## **使い方**  

1. シーン内に `Transmitter` と `Receiver` を任意の場所に配置します。  
2. カスタムイベント `Activate` および `Deactivate` を呼び出し、プレイヤーの操作で `frequency` 変数を設定します。  
3. シーンに `UdonRadioCommunication` を1つ追加します。  

詳細な使い方や `Transceiver` の例については、 `Demo.unity` シーンを参照してください。  

---

## **オプションの依存関係**  

| 名前 | 説明 |  
| :-- | :-- |  
| [InariUdon](https://github.com/esnya/InariUdon.git) | `Interaction/TouchSwitch` と `Interaction/KeyboardInput` が使用され、**サンプルプレハブに必須**です。 |  

---

## **ランタイムの負荷**  
`Update` ループを使用するUdonは1つだけです。  
- **トランスミッター（`Transmitters`）の数**を `Nt`  
- **レシーバー（`Receivers`）の数**を `Nr`  
- **プレイヤー（`Players`）の数**を `Np`  
とすると、計算量は `O(Np(Nt+Nr))` となります。  

---

## **設定項目**  

### **トランシーバー（Transceiver）**  
| プロパティ名 | 説明 |  
| :-- | :-- |  
| Exclusive | 送信中にレシーバーをオフにします。 |  

### **レシーバー（Receiver）**  
| プロパティ名 | 説明 |  
| :-- | :-- |  
| Sync | チェックすると、レシーバー付近の全員が無線を聞くことができます。チェックを外すと、ローカルクライアントのみ聞けます。 |  

---

## **SaccFlightとの統合**  
SaccFlightAndVehicles向けの統合アドオンを提供しています。  
DFUNCs（Dynamic Functions）を使用して、周波数の管理、受信の切り替え、Push-to-Talk機能を操作できます。  

![SaccFlight統合イメージ](https://user-images.githubusercontent.com/2088693/219712019-99885e55-98cc-4578-8931-456da063de62.png)  

---

## **インストール方法**  

1. メニューの **Window** → **Package Manager** を開きます。  
2. 「+」ボタンをクリックし、**`Add package from git URL`** を選択します。  
3. 以下のURLを入力して「Add」ボタンをクリックします。  
   - **安定版リリース**:  
     `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications-sf`  
   - **ベータ版リリース**:  
     `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications-sf#beta`  