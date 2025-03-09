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
   - **リリース**:  
     `git+https://github.com/itounagi0116/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications`  
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

---

## LLMの補足

esnya/UdonRadioCommunications は、VRChatのUdonワールド向けに開発された簡易的な無線通信システムです。このプロジェクトは、仮想空間内でのリアルタイム音声通信を実現し、特に航空機シミュレーションや車両操作との連携に特化した機能を提供します。以下に詳細を解説します：

---

### **1. プロジェクト概要**
- **目的**: VRChatワールド内で、現実の無線通信に近い体験を再現するために開発されました。周波数設定や送受信の制御を通じ、複数プレイヤー間の音声通信を可能にします。
- **特徴**:
  - **軽量化**: Udonの計算負荷を考慮し、1つのUdonのみがUpdateループを使用する設計。
  - **柔軟な設定**: 送信機（Transmitter）と受信機（Receiver）を自由に配置し、周波数や同期方法をカスタマイズ可能。
  - **SaccFlightAndVehicles連携**: 航空機/車両シミュレーターとの統合をサポートし、Push-To-Talk（PTT）機能を提供。

---

### **2. 主要コンポーネント**
- **Transmitter（送信機）**: プレイヤーが音声を送信するための装置。`DFUNC_URC_PTT.prefab` はPTT機能を実装したプレハブで、デスクトップキー（デフォルトはF1キー）で送信を制御します。
- **Receiver（受信機）**: 特定の周波数に合わせた音声を受信する装置。「Exclusive」モードでは送信中に受信を自動停止します。
- **UdonRadioCommunication**: シーンに1つ配置する中核コンポーネント。通信の同期と管理を担います。

---

### **3. インストール手順**
1. **Unityプロジェクト設定**:
   - VRChat Creator CompanionでUdonSharpを含むプロジェクトを作成。
   - UnityのPackage ManagerからGit URLを追加：  
     `git+https://github.com/esnya/UdonRadioCommunications.git?path=/Packages/com.nekometer.esnya.udon-radio-communications`  
     （ベータ版は `#beta` を末尾に追加）。
2. **オプション依存関係**:
   - SaccFlightAndVehicles連携用パッケージは別途追加が必要。

---

### **4. 使用方法**
- **基本設定**:
  - 送信機と受信機をシーン内に配置。
  - カスタムイベント `Activate`/`Deactivate` で通信の有効化・無効化を制御。
  - 変数 `frequency` で周波数を設定。
- **同期オプション**:
  - `Sync` を有効にすると、近くのプレイヤー全員が受信可能。無効時はローカルクライアントのみ。
- **パフォーマンス**:
  - 計算量は `O(Np(Nt + Nr))`（プレイヤー数×送受信機数の合計）で、大規模ワールドでは最適化が推奨されます。

---

### **5. 技術的詳細**
- **スクリプト**: UdonSharpを使用し、`MonoBehaviour` を拡張して通信ロジックを実装。
- **キーバインド**: `desktopKey` プロパティでPTTキーをカスタマイズ可能（例：112はF1キーに対応）。
- **依存ライブラリ**: InariUdonのインタラクションコンポーネントがサンプルプレハブで使用されます。

---

### **6. 応用例**
- **航空機シミュレーター**: コックピット内の無機体感を強化。
- **多人数協調プレイ**: チーム間の戦略的な音声通信を実現。
- **イベント空間**: アナウンスシステムとしての活用。

---

### **7. 参考リソース**
- **デモシーン**: リポジトリ内の `Demo.unity` で動作確認可能。
- **作者情報**: 開発者esnyaは日本在住で、VRChat向けUdonツールを多数公開しています。

このプロジェクトは、GitHubでMITライセンスの下で公開されており、自由に改変・再配布が可能です。詳細は[公式リポジトリ](https://github.com/esnya/UdonRadioCommunications)を参照してください。
