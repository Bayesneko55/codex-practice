# 研究計画書（下書き）

## 1. 背景

網膜血管は分岐・接続を持つネットワークであり、眼底画像からその形態を観察できる。一方、低コントラストや血管の重なりにより、画像上で一部の血管が不明瞭になる。血管領域を抽出するだけでなく、欠けた接続の候補と推定の不確実性を示すことが重要である。そこでベイズ統計を用い、欠損リンクの存在確率とその根拠を評価する。

## 2. 問い

網膜血管ネットワークの欠損リンクを、ベイズロジスティック回帰でどの程度推定できるか。また、リンクの事後確率と係数の事後分布を用い、予測の不確実性や判断に寄与する特徴を説明できるかを問う。

## 3. 先行研究

Staalらの “Ridge-based vessel segmentation in color images of the retina”（2004）はDRIVEを用いた網膜血管抽出法を報告した。Hoover、Kouznetsova、Goldbaumの “Locating blood vessels in retinal images by piecewise threshold probing of a matched filter response”（2000）はSTAREを用いて血管検出法を検証した。リンク予測では、Liben-NowellとKleinbergの “The Link-Prediction Problem for Social Networks”（2007）が共通近傍等の指標を整理している。またRibeiroらの “Why Should I Trust You?: Explaining the Predictions of Any Classifier”（2016）は、個別予測を説明するLIMEを提案した。本研究では、網膜血管グラフのリンク予測にベイズモデルを適用し、事後確率と特徴の寄与を併せて評価する。

## 4. 方法

データは血管領域の手動ラベルを含む公開眼底画像DRIVEとし、可能であればSTAREでも検証する。血管マスクを細線化し、端点・分岐点をノード、血管区間をエッジとするグラフに変換する。グラフからエッジを除いて欠損を模擬し、ランダム削除を基本に、局所構造に応じた条件も検討する。削除したエッジの両端点を候補とし、距離、共通隣接ノード数、局所次数を説明変数にベイズロジスティック回帰を適用する。弱情報事前分布を置き、MCMCで係数の事後分布を推定する。ROC-AUCとBrierスコアで予測性能・確率校正を評価する。候補ごとの事後確率・信用区間と係数の事後分布を示し、各特徴の寄与と不確実性を説明する。

## 5. 現在までの結果と今後の計画

現時点では計画の整理段階で、解析結果はまだない。今後、グラフ化と欠損生成の手順を確定し、モデル推定とAUC・Brierスコアによる評価を行う。事後確率が曖昧な接続や誤推定を示すかを調べ、必要に応じて非ベイズ手法とも比較し、不確実性評価を説明に用いる利点と限界を明らかにする。

### 参考文献

- Staal, J. et al. “Ridge-based vessel segmentation in color images of the retina.” *IEEE Transactions on Medical Imaging*, 2004.
- Hoover, A., Kouznetsova, V., and Goldbaum, M. “Locating blood vessels in retinal images by piecewise threshold probing of a matched filter response.” *IEEE Transactions on Medical Imaging*, 2000.
- Liben-Nowell, D. and Kleinberg, J. “The Link-Prediction Problem for Social Networks.” *JASIST*, 2007.
- Ribeiro, M. T., Singh, S., and Guestrin, C. “Why Should I Trust You?: Explaining the Predictions of Any Classifier.” *KDD*, 2016.
