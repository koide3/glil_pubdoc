# Important parameters

特に調整が必要となるパラメータを抜粋して説明する．[Detailed parameters](params_detail.md)を併せて参照すること．

## Config files & ROS params

GLIL では一度設定した後は頻繁には変更しないパラメータ (e.g., センサ設定，推定パラメータ設定) の設定にはConfigファイルを使用し， オペレーション毎に変更しうるパラメータ (e.g., 地図ファイル，初期姿勢) の設定にはROS paramを使用する．

!!!tip
    起点ファイルはROS paramの```config_path```を設定することで変更できる (```config_path + "/config.json"```が起点ファイルとなる)．```config_path```の最初の位置文字が ```/```(スラッシュ) から始まる場合は絶対パスとして解釈され，それ以外の場合は```glil_ros```のパッケージパスに対する相対パスとして解釈される．

!!!tip
    ROS2の仕様上，Configファイルは```ros2_ws/install/glil_ros/share/glil_ros/config```以下に配置する必要があるため，```glil_ros/config```以下のファイルへの変更を適用するためには```colcon build```を実行する必要がある．

## ROS params (glil_ros.launch.py)

| Parameter            | Description |
| -----------------    | ----------- |
| map_load_mode        | 地図読み込みモード (```POINTCLOUD``` or ```BINARY```)． |
| map_path             | 地図データパス |
| init_by_params       | ```true```の場合，初期姿勢をROS paramから与える．```false```の場合，地図に対してGroundingされていない状態で推定を開始する． |
| init_T_world_imu     | 地図に対する初期IMU姿勢 (```tx,ty,tz,qx,qy,qz,qw```)．※数字の間にスペースを入れてはならない． |


## Config files

!!!warn
    Details of this section are revealed for only closed-source users.


### ROS関連 (config_ros.json)

### センサ設定 (config_sensors.json)

### 点群前処理設定 (config_preprocess.json)

### GPUベースオドメトリ推定設定 (config_frontend_gpu.json)

### グローバルマップ前処理設定 (config_globalmap.json)
