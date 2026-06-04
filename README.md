# BLDC Motor 6-Step Commutation Visualizer

BLDCモータの6ステップ台形波転流を、回路図・BEMF波形・ロータ断面図でインタラクティブに学べるWebアプリです。

🔗 **[Live Demo](https://kota-may478.github.io/bldc-visualizer/)**

---

## 機能

- **ロータ断面図** — 4極(2極対)モータのN-S-N-S十字型磁石が電気角に合わせてリアルタイム回転。コイルの電流方向（●=手前, ×=奥）も表示
- **BEMF波形** — 3相の台形波BEMF、ZC検出点・転流点・+30°タイミングを正確に表示。トルク概念波形（紫）も重ねて表示
- **三相インバータ回路図** — PWM ON（主電流）・OFF（LS-BD還流）・転流瞬間（HS-BD回生）の3タイミングを切り替え
- **ゲート信号** — 1電気周期全6ステップのPWMゲート信号（現在ステップを強調）
- **物理説明パネル** — 各ステップ・各相のBEMFと鎖交磁束の物理的根拠を詳述
- **自動再生** — ▶ボタンでロータが連続回転

---

## 理論的正確性

| 項目 | 内容 |
|---|---|
| 極数 | 4極（2極対）: 電気角 = 機械角 × 2 |
| BEMFオフセット | U=150°, V=90°, W=30°（全ステップ中盤でZC=0を数値検証済み） |
| ZCタイミング | ステップ中盤(el[0]+30°)で監視相BEMFがゼロクロス |
| 転流点 | ZC検出から30°後 = 次ステップ開始（トルク最大の平坦域中央） |
| LS-BD還流 | srcローサイドBDがGND→srcノード方向に導通（Vbus不使用） |
| HS-BD回生 | フロート相HSのBDがmonノード→Vbus方向に導通（monノード電位がVbus超え） |
| コイル配置 | U+=90°, V+=210°, W+=330°（機械角、ステータ固定） |

---

## ローカルで動かす

```bash
git clone https://github.com/kota-may478/bldc-visualizer.git
cd bldc-visualizer
# index.html をブラウザで直接開くだけ（サーバー・Node.js 不要）
open index.html
```

## GitHub Pages で公開する

1. このリポジトリを GitHub に push する
2. Settings → Pages → Source を `main` ブランチの `/ (root)` に設定
3. Save → 数分後に `https://kota-may478.github.io/bldc-visualizer/` で公開される

---

## 技術仕様

| 項目 | 内容 |
|---|---|
| 実装 | 単一HTMLファイル（CSS・JS内包） |
| 外部依存 | Google Fonts のみ（オフラインでも動作） |
| フレームワーク | なし（ネイティブCanvas 2D API） |
| アニメーション | requestAnimationFrame |

---

## 参考文献

- [Microchip AN1913](https://www.nxp.com/docs/en/application-note/AN1913.pdf): 3-phase BLDC Motor Control with Sensorless Back-EMF
- [TI SPRABZ4](https://www.ti.com/lit/an/sprabz4/sprabz4.pdf): Trapezoidal Control of BLDC Motors
- [MathWorks Six-Step](https://www.mathworks.com/help/mcb/gs/six-step-commutation.html): Six-Step Commutation of BLDC Motor

## License

MIT
