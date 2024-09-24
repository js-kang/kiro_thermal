# kiro_thermal
열영상내 사람 검출 알고리즘

Thermal Detection (20.04, ROS Foxy)
======================================================================================
0. 설치 전 초기 작업 

> jetson stats 설치
	sudo apt update
	sudo apt upgrade
	sudo apt install python3-pip
	sudo -H pip install -U jetson-stats
	sudo reboot	


> 설치완료 후, jetson-stats 실행 확인
	jtop

==========================================================================================================
1. CUDA 및 OpenCV 설치

> OpenCV & CUDA 설치 (6시간 소요)
	git clone https://github.com/mdegans/nano_build_opencv.git
	cd nano_build_opencv/
	gedit build_opencv.sh
		113 line -D CUDNN_VERSION='8.0' -> '8.6' 으로 수정 후 저장
	
	./build_opencv.sh 4.5.4

> OpenCV & CUDA 확인
	jtop
		정상 설치가 완료 되었을때: INFO Libraries OpenCV: 4.5.4 with CUDA: YES

==========================================================================================================	
	
> (가상환경 필요한 경우)
	sudo su
	virtualenv -p python3.8 thermal_detection
	source thermal_detection/bin/activate
	
==========================================================================================================
2. 필수패키지 설치
> torchvision 설치
	git clone https://github.com/pytorch/vision torchvision
	cd torchvision
	git checkout v0.15.2
	python3 setup.py install --user
	
		PYTHON PATH error 해결방법: export PYTHONPATH="${PYTHONPATH}:(파이썬라이브러리경로 or 가상환경)/lib/python3.8/site-packages/"
		설정 후, 재시도 python3 setup.py install --user

==========================================================================================================
3. 학습 모델 및 실행 소스 다운로드

> detection source & model 설치
	git clone https://github.com/js-kang/kiro_thermal.git
	python kiro_thermal/setup_env.py
		
==========================================================================================================
4. 알고리즘 실행
> detection 알고리즘 실행
	yolo detect predict --model=thermal_light_kiro.pt --source=0 --show=True
	

==========================================================================================================

==========================================================================================================
