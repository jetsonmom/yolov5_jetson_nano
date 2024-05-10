# yolov5_jetson_nano

######  참고 링크 https://blog.naver.com/tory0405/223246391729

###### 잘 되던게 github 정리하려고 다시 시작했는데 안된다. 경험하지 않은 에러가 속출한다. 그 내용은 블로그에 정리를 하였다. 에러가 많아서 무척 길고 해결에 많은 시간이 필요했다https://blog.naver.com/jmerrier/223392057106 그리고 다시 정리한다. 제타님이 처음부터 가상에서 한 점이 나랑 다르다. 그래서 가상에서 하였다.  참고 https://medium.com/@scofield44165/jetson-nano-dev-kit%E4%B8%AD%E5%AE%89%E8%A3%9Darchiconda-install-archiconda-in-jetson-nano-dev-kit-1e695326596f
[https://blog.naver.com/zeta0807](https://blog.naver.com/zeta0807/223382438975?trackingCode=blog_bloghome_searchlist)
``` python
uycgb
```


###### yolo 가상환경 만들기
``` bash
uname -a
wget https://github.com/Archiconda/build-tools/releases/download/0.2.3/Archiconda3-0.2.3-Linux-aarch64.sh


sudo chmod 755 Archiconda3-0.2.3-Linux-aarch64.sh
````

``` bash
 ls
````
###### 결과
ldh@ldh-desktop:~$ ls
Archiconda3-0.2.3-Linux-aarch64.sh  Downloads         Pictures   yolov5
Desktop                            examples.desktop  Public
docker_dli_run.sh                  Music             Templates
Documents                          nvdli-data        Videos


``` bash
 ./Archiconda3-0.2.3-Linux-aarch64.sh
```
###### 실행 중 선택하라고 나온다.
설치 프로그램 진행 방법
./Archiconda3-0.2.3-Linux-aarch64.sh 실행이미 실행 중인 상태이므로 바로 다음 단계로 넘어갑니다.
라이선스 스크롤링라이선스 텍스트를 모두 읽거나 빠르게 넘기고 싶다면 [q] 키를 누르세요. 텍스트가 모두 표시될 때까지 Enter 키를 계속 누를 수도 있습니다.
설치 경로 지정 및 설치 완료설치 경로를 입력하라는 메시지가 나타납니다. 기본 경로를 사용하려면 [Enter] 키를 눌러 계속하세요.
환경 변수 설정설치가 완료되면 터미널에서 conda 명령을 사용하기 위해 다음과 같이 .bashrc에 경로를 추가하세요.
yes--->
enter --->
yes
in your /home/ldh/.bashrc ? [yes|no]
[no] >>> yes



###### result 
installing: cryptography-2.5-py37h9d9f1b6_1 ...
installing: wheel-0.32.1-py37_0 ...
installing: pip-10.0.1-py37_0 ...
installing: pyopenssl-18.0.0-py37_0 ...
installing: urllib3-1.23-py37_0 ...
installing: requests-2.19.1-py37_0 ...
installing: conda-4.5.12-py37_0 ...
installation finished.
Archiconda가 ~/archiconda3 폴더에 설치되어 있음을 확인했으므로, 해당 경로를 환경 변수에 추가하여 conda 명령을 사용할 수 있도록 해보겠습니다.
Archiconda 경로 추가
다음 명령을 실행하여 Archiconda의 bin 폴더를 환경 변수에 추가합니다.
``` bash
# Archiconda 경로를 환경 변수에 추가
echo 'export PATH="$HOME/archiconda3/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# conda 업데이트
conda update conda

# conda init 및 초기화
conda init bash
source ~/.bashrc

# 가상 환경 생성 및 패키지 설치
conda create -n yolov5 python=3.8
conda activate yolov5
pip install -r ~/yolov5/requirements.txt
```
# Do you wish the 

``` bash
 conda activate yolov5
```

###### 결과 가상에서 설치 torch, torchvosion 다운로드
(yolo) dli@dli:~$ 

``` bash
 pip install -U pip wheel gdown

 gdown https://drive.google.com/uc?id=1hs9HM0XJ2LPFghcn7ZMOs5qu5HexPXwM

 gdown https://drive.google.com/uc?id=1m0d8ruUY8RvCP9eVjZw4Nc8LAwM8yuGV
```
아래 두 라인을 실행(library 설치) 후 torch, torchvision은 확인이 가능하였다.
``` bash
sudo apt-get install libopenblas-base libopenmpi-dev
sudo apt-get install libomp-dev
```
``` bash
(yolo) dli@dli:~$ python
Python 3.8.13 | packaged by conda-forge | (default, Mar 25 2022, 05:56:18) 
[GCC 10.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
/home/dli/archiconda3/envs/yolo/lib/python3.8/site-packages/torch/_masked/__init__.py:223: UserWarning: Failed to initialize NumPy: No module named 'numpy' (Triggered internally at  /pytorch/torch/csrc/utils/tensor_numpy.cpp:68.)
  example_input = torch.tensor([[-3, -2, -1], [0, 1, 2]])
>>>
```

###### 위의 에러는 numpy 다운로드 안되어 있어서 에러 발생
``` bash
 conda install numpy                                       # 또는 >>> 다음에 설치를 해도 된다.
```
after download -> install
``` bash
pip install torchvision-0.12.0a0+9b5a3fe-cp38-cp38-linux_aarch64.whl
pip install torch-1.11.0a0+gitbc2c6ed-cp38-cp38-linux_aarch64.whl
```
``` bash

(yolo) dli@dli:~$ python

>>> import torch
>>> import torchvision
>>> print(torch.__version__)
>>> print(torchvision.__version__)
>>> print("cuda used", torch.cuda.is_available())
cuda used True
>>> 
```
``` bash
git clone https://github.com/Tory-Hwang/Jetson-Nano2
```
``` bash
(yolo) dli@dli:~$ cd Jetson-Nano2/
(yolo) dli@dli:~/Jetson-Nano2$ cd V8
(yolo) dli@dli:~/Jetson-Nano2/V8$ pip install ultralytics
(yolo) dli@dli:~/Jetson-Nano2/V8$ pip install -r requirements.txt 
(yolo) dli@jdli:~/Jetson-Nano2/V8$ pip install ffmpeg-python
```
######  yolov8n.pt 다운로드
https://github.com/ultralytics/ultralytics?tab=readme-ov-file
위의 링크에서 다운로드 받았다.
경로는 (yolo) dli@jetson:~/Jetson-Nano2/V8

!![제목 없음](https://github.com/jetsonmom/yolov8_jetson4GB/assets/92077615/d687b7ea-5889-466e-83cb-a249954658f1)

!![Screenshot from 2024-03-24 23-44-20](https://github.com/jetsonmom/yolov8_jetson4GB/assets/92077615/89dc7fc0-fc81-48ba-8268-e9b7667e04f7)

!![Screenshot from 2024-03-24 23-50-56](https://github.com/jetsonmom/yolov8_jetson4GB/assets/92077615/bb772518-fb6a-4f07-a4af-b340ff53e476)



###### USB camera를 연결하였다. 그러나 전혀 Yolo를 실행하는 화면이 보이지 않았다. 이유는 토리삼촌과 나의 환경이 달라서이다. 코드 수정해야한다.
``` bash
gedit  detectY8.py
```

(yolo) dli@jetson:~/Jetson-Nano2/V8$ python detectY8.py 

###### 코드를 보니 rtsp가 기본으로 되어있다. 그래서 rtsp를 사용하지 않도록 변경했다.
!![Screenshot from 2024-03-25 12-58-30](https://github.com/jetsonmom/yolov8_jetson4GB/assets/92077615/3883ca74-efd7-4e92-9888-89b40a9e01bd)


def predict(cfg=DEFAULT_CFG, use_python=False):
    brtsp = True
-> 
    brtsp = False
detectY8.py 스크립트에서 RTSP(Remote Desktop Protocol)를 사용하지 않도록 변경하려면, brtsp = True 라인을 찾아 False로 변경해야 합니다. 이 변경은 스크립트가 RTSP 스트리밍 대신 다른 비디오 입력 소스(예: USB 카메라)를 사용하도록 지시합니다. 코드에서 brtsp 변수가 RTSP 스트리밍을 활성화하거나 비활성화하는 데 사용되는 것으로 보입니다.


``` bash
(yolo) yolo@yolo-desktop:~/Jetson-Nano2/V8$ python detectY8.py
```
!![Screenshot from 2024-03-25 13-23-47](https://github.com/jetsonmom/yolov8_jetson4GB/assets/92077615/f84b0a67-571e-45aa-969e-4e6e8188a0b8)





