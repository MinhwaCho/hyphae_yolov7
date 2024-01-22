## 1. Installation
### 1-1. Yolov7 모델 install
참고: <https://github.com/WongKinYiu/yolov7.git>

### 1-2. 환경 설정
- python 3.8
- pip install -r requirements.txt
- pip install setuptools==59.5.0
- CUDA 버전에 맞는 pytoch gpu 설치 (optional)
  (예시: pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html)

## 2. Test
### 2-1. 테스트할 데이터셋(이미지) 저장
- 이미지 640 x 640으로 resize
- 디렉터리 생성 후 이미지 저장 (예: data/test/images)

### 2-2. 테스트 결과
```
python detect.py --weights runs/train/yolov7-custom/weights/best.pt -- source ./data/test/images --save-txt --save-conf
```
- weights: weight 파일 경로 (yolov7-custom)
- source: 테스트 파일 경로
- 테스트 파일 결과 저장 경로 => runs/detect/exp

  ### 2-3. 테스트 결과 해석
  - runs/detect/{테스트_이미지_저장_디렉터리} 에 위치한 이미지
 
  - runs/detect/{테스트_이미지_저장_디렉터리}/labels
    
&nbsp;&nbsp; 예시: 3 0.34375 0.220313 0.01875 0.028125 0.256104

&nbsp;&nbsp; - 구성: 카테고리종류, center_x, center_y, width, height, confidence

&nbsp;&nbsp; - 이때, (center_x, center_y, width, height) 는 0~1 사이의 값; 이미지 사이즈 크기로 나누어 정규화된 값

&nbsp;&nbsp; - 카테고리종류는 data.yaml에서 확인 가능 (예: 0 = CONTAM, 1 = aging, 2 = imbalance, 3 = watermark)

&nbsp;&nbsp; - Confidence는 검출한 것에 대한 정확도
