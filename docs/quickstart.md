# Getting started

## Prerequisite

1. [Installation](installation.md) に従い， GLIL のインストールを行う．
2. [テストデータ (rosbag)](https://zenodo.org/record/7233945)をダウンロードする．  
    ROS1: [os1_128_01_downsampled.bag (515MB)](https://zenodo.org/record/7233945/files/os1_128_01_downsampled.bag?download=1) or [os1_128_01.bag (7.3GB)](https://zenodo.org/record/7233945/files/os1_128_01.bag?download=1)  
    ROS2: [os1_128_01_downsampled.tar.gz (426MB)](https://zenodo.org/record/7233945/files/os1_128_01_downsampled.tar.gz?download=1) or [os1_128_01.tar.gz (3.2GB)](https://zenodo.org/record/7233945/files/os1_128_01.tar.gz?download=1)
3. [地図データ (PLY or PCD)](https://zenodo.org/record/7961649)をダウンロードする．  
    PLY: [os1_128.ply](https://zenodo.org/record/7961649/files/os1_128.ply?download=1)  
    PCD: [os1_128.pcd](https://zenodo.org/record/7961649/files/os1_128.pcd?download=1)

## Try it!

1. ```launch/glil_ros.launch.py``` 内の地図データファイルパスと初期姿勢パラメータを以下のように設定する．

    ```python
      parameters=[
        {
          ...
          'map_load_mode': 'POINTCLOUD',
          'map_path': '/path/to/os1_128.ply',
          ...
          'init_by_params': True,
          'init_T_world_imu': '0.011,-0.033,0.078,0.109,-0.042,-0.006,0.993'
        }
      ]
    ```

2. GLIL を起動する．地図の読み込み処理が終了し，ビューワ上に地図点群が表示されるのを待つ．

    ```bash
    cd glil_ros/launch
    ros2 launch ros2 launch glil_ros.launch.py
    ```

    !!!tip
        地図データに点群ファイル(PLY or PCD)を設定した場合には，点の共分散推定とボクセルマップ生成の処理に時間がかかる．```save_binary_map```に```True```をセットしておくと前処理後の地図が```binary_map_save_path```に保存されるため，以降は```map_load_mode```を```BINARY```に変更し，```map_path```を保存したバイナリ地図データパスに設定することで起動時間を短縮することができる．


3. 別のコンソールでテストデータを再生する．

    ```bash
    ros2 bag play os1_128_01
    ```

    <div class="youtube">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/UiB6NqdHncI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
    </div>

4. Rviz2 で表示する．

    ```bash
    cd glil_ros/rviz
    rviz2 -d glil_ros2.rviz
    ```

    <div class="youtube">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Io0buHhiwyg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
    </div>


## Localization on a severely cropped map

PLY: [os1_128_cropped.ply](https://zenodo.org/record/7972321/files/os1_128_cropped.ply?download=1)  

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/k8Vpqbrv7Js" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>