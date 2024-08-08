# Introduction

## :fontawesome-solid-exclamation: Warning

本ドキュメントは産総研で開発された**Closed-source 点群自己位置推定パッケージ**に関するドキュメントです． 知財開示に興味のある方は [k.koide@aist.go.jp](k.koide@aist.go.jp) までご連絡ください．  
なお，ベースとなる地図生成パッケージがOSSとして公開されています : https://github.com/koide3/glim．

This documentation is about a **closed-source point-cloud-based localization package**. If you are interested in the licensing of this package, please send a mail to [k.koide@aist.go.jp](k.koide@aist.go.jp) .  
Note that a mapping package, which shares the same base algorithm with this package, is available as open source : https://github.com/koide3/glim.

## :fontawesome-solid-location-crosshairs: GLIL: Robust Localization on a 3D Prior Map

***GLIL*** は LiDAR-IMU タイトカップリングに基づく三次元既知地図上でのセンサ姿勢推定パッケージである．GPUを利用した高速な点群マッチングをベースに構築されており，従来手法に対して以下のような特徴を持つ．

- LiDAR制約とIMU制約の同時最適化によって急激な動きに対して頑強
- 自己運動量推定と地図とのマッチングを同時に行うことで，地図の欠損や変化に対して頑強
- 点群とIMUが計測可能なほぼすべてのセンサで利用可能
- モジュール間通信 (Global callback slots) によって，追加センサ制約などを容易に追加可能

また，サポートは限定的であるが実験的機能として以下の機能を有する．

- CPUのみを使った自己位置推定 (GPU版と比較して若干低可搬性)
- 初期化・自己位置再認識のための大域姿勢推定機能


## :material-ubuntu: Supported environments

GLIL は Ubuntu 20.04 (ROS galactic/noetic) 以降でビルド可能であるが，重点的にテストを行っている Ubuntu 22.04 (ROS humble) での利用を推奨する．また， CUDA 12.0 以降の利用を推奨する．

## :fontawesome-solid-video: Video

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Ry5SiLU-LDM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

<br>

<div class="youtube">
<iframe width="560" height="315" src="https://www.youtube.com/embed/k8Vpqbrv7Js" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

## :material-file-document: Documentation

- [Doxygen generated API (Available for only closed-source users)](https://not_available)


!!!tip
    API リストの最新版は glil_ros のソースコードから doxygen を利用して生成できる．
    ```bash
    cd glil_ros
    doxygen Doxyfile
    ```

!!!tip
    本ドキュメントの最新版は glil_ros のソースコードから mkdocs を利用して閲覧することができる．

    1. mkdocs のインストール

        ```bash
        pip install mkdocs mkdocs_material
        ```

    2. mkdocs server の起動

        ```bash
        cd glil_ros
        mkdocs serve
        ```

    3. ブラウザで ```127.0.0.1:8000``` にアクセスする．


## :simple-googlescholar: Related work

- 小出健司, 大石修士, 横塚将志, 阪野貴彦, "点群・IMU制約のウィンドウ最適化に基づく既知地図上での6DoF姿勢推定", ROBOMECH2023 [:fontawesome-solid-file-pdf:](https://staff.aist.go.jp/k.koide/assets/pdf/robomech2023.pdf)
- Kenji Koide, Shuji Oishi, Masashi Yokozuka, and Atsuhiko Banno, "Tightly Coupled Range Inertial Localization on a 3D Prior Map Based on Sliding Window Factor Graph Optimization", ICRA2024 [:fontawesome-solid-file-pdf:](https://staff.aist.go.jp/k.koide/assets/pdf/icra2024_02.pdf)
- Kenji Koide, Masashi Yokozuka, Shuji Oishi, and Atsuhiko Banno, "Globally Consistent and Tightly Coupled 3D LiDAR Inertial Mapping", ICRA2022 [:fontawesome-solid-file-pdf:](https://staff.aist.go.jp/k.koide/assets/pdf/icra2022.pdf)

## :fontawesome-solid-envelope: Contact

Kenji Koide [:material-home:](https://staff.aist.go.jp/k.koide/) [:material-mail:](mailto:k.koide@aist.go.jp) [:material-twitter:](https://twitter.com/k_koide3)
National Institute of Advanced Industrial Science and Technology (AIST), Japan