## 何を実施したか

metal_nut データセットにおいて、異常検知を実施する。

## 環境構築

1. 以下のコマンドで docker イメージを作成する(docker compose のバージョンが 2 系列の場合は、ハイフンの代わりに半角スペースとすること)。

   ```
   docker-compose build
   ```

2. 以下のコマンドで jupyternotebook を起動して、`localhost:8888` にアクセスする(docker compose のバージョンが 2 系列の場合は、ハイフンの代わりに半角スペースとすること)。

   ```
   docker-compose up
   ```

3. `./notebooks/anormaly_detection.ipynb`にアクセスして上から順にセルを実行する。

## 使用した手法について

https://arxiv.org/abs/2005.14140 の手法を使用した。

簡単なアルゴリズムは下記の通り

1. 学習データを入力としたときの学習済み EfficientNet の中間層の出力を特徴量として取得

2. 取得した特徴量の平均と分散共分散行列を計算

3. 求めたい画像の特徴量と、手順 2 で求めた平均と分散共分散行列からマハラノビス距離を計算する。

利点としては、下記の通り、学習が不要であることが挙げられる。

学習が不要(学習用データから特徴量の統計量を取得する処理を学習と呼ぶのならば学習は必要となる。ただし、統計量を一度計算してストレージ内に保存しておけば再利用可能である。)

## 参考

- https://arxiv.org/abs/2005.14140

- https://qiita.com/shinmura0/items/5f2c363812f7cdcc8771 実装の参考 1

- https://qiita.com/sUeharaE4/items/023455822376c07cd6ef 実装の参考 2

- https://datawokagaku.com/f1score/ しきい値を決める際に参考にした
