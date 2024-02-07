# Viewers and ROS interface

GLIL では二種類のビューワ (標準ビューワとRvizビューワ) を提供する．いずれも ```config_ros.json``` の ```extension_modules``` 内の対応するモジュール名を追加/削除することで有効化/無効化することができる．

## Standard viewer

標準ビューワは GLIL の起動と同時に立ち上がり，推定状態の確認や地図に対する姿勢の設定を行うことができる．

### 高さクリッピング

```clip_by_z``` チェックボックスを有効にすると，地図点群を高さに応じてフィルタリングして表示する．表示範囲は ```z_range``` スライダーによって変更する．

### 推定状態表示

```Status``` ボタンを押すことで推定状態表示ウィンドウが表示され，以下の情報が表示される．

| Label    | Description  |
| -------- | ------------ |
| frame ID | 最新フレームのID [int] |
| stamp    | 最新フレームのタイムスタンプ [s] |
| points   | 最新フレームの点数 |
| T_w_i    | IMU姿勢 (```T_world_imu = [tx, ty, tz, qx, qy, qz, qw]```) |
| v_w_i    | IMU速度 (```v_world_imu = [vx, vy, vz]```) |
| bias     | IMUバイアス (```bias = [ax, ay, az, wx, wy, wz]```) |

### 手動初期姿勢設定

```Manual align``` ボタンを押すことで手動姿勢設定モーダルを表示する．

### 動画

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/UiB6NqdHncI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

## Rviz viewer

Rviz viewer は推定結果を基に各種のROSメッセージを publish/subscribe する．

### ROS params

| Name                   | Description  |
| --------               | ------------ |
| map_frame              | 地図フレームID (Grounded 状態の時のフレームID) |
| odom_frame             | オドメトリフレームID (Ungrounded 状態の時のフレームID) |
| imu_frame              | IMUフレームID |
| publish_tf             | `True` の場合，map_frame -> imu_frame のTFフレームを出力する． |

### Published topics

| Topic                  | Type                        | Description  |
| --------               | ----                        | ------------ |
| ~global_map            | PointCloud2                 | 地図点群 |
| ~imu_pose              | PoseStamped                 | 推定IMU姿勢 |
| ~imu_pose_with_cov     | PoseWithCovarianceStamped   | 推定IMU姿勢 + 共分散行列 |
| ~marginalized_imu_pose | PoseStamped                 | 周辺化されたIMU姿勢 (最適化ウィンドウから出た姿勢変数) |
| ~twist                 | TwistStamped                | 推定IMU速度 |
| ~points                | PointCloud2                 | 前処理されたLiDAR点群 |
| ~aligned_points        | PointCloud2                 | 地図座標に変換されたLiDAR点群 |

### Subscribed topics

※ [Initialization proceduce: 2. ROS topics](initialization.md) も参照

| Topic                  | Type                        | Description  |
| --------               | ----                        | ------------ |
| ~initialpose           | PoseWithCovarianceStamped   | 地図に対するIMU姿勢 (共分散は使用しない)．与えられた姿勢から地図に対してスキャンマッチングした結果を入力姿勢として利用する． |
| ~initialpose_noalign   | PoseWithCovarianceStamped   | 地図に対するIMU姿勢 (共分散は使用しない．スキャンマッチングを行わない．) |

### 動画

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Io0buHhiwyg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>
