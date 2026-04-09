# Image-Formation-with-Python


간단한 카메라 캘리브레이션 및 왜곡 보정(OpenCV) 실습 폴더입니다.

## 폴더 구성

- `camera_calibration.py`: 체스보드 이미지에서 코너를 검출해 카메라 내부 파라미터와 왜곡 계수를 계산합니다.
- `distortion_correction.py`: 저장된 캘리브레이션 결과를 사용해 이미지/영상 왜곡을 보정합니다.
- `data/chessboard/`: 캘리브레이션 입력용 체스보드 사진 폴더입니다.
- `calibration_result.npz`: 캘리브레이션 결과 파일(카메라 행렬 K, 왜곡 계수 등)입니다.
- `distortion_results/`: 왜곡 보정 전/후 비교 결과 이미지들이 저장되는 폴더입니다.

## 실행 순서

1. 캘리브레이션 실행

```bash
python camera_calibration.py
```

2. 왜곡 보정 실행(이미지)

```bash
python distortion_correction.py --mode image --input data/chessboard/chess_*.jpg --output distortion_results --calib calibration_result.npz
```

## 결과물 설명

- `calibration_result.npz`
  - `K`: 카메라 행렬
  - `dist_coeff`: 렌즈 왜곡 계수
  - `rms`, `mean_reprojection_error`: 캘리브레이션 품질 지표
  - `used_files`: 실제로 사용된 이미지 목록
- `distortion_results/distortion_results_01.jpg` ~ `distortion_results/distortion_results_05.jpg`
  - 각 결과 이미지의 좌측: 원본 체스보드 이미지
  - 각 결과 이미지의 우측: 왜곡 보정 이미지

## 사진 미리보기

### 왜곡 보정 결과 이미지

![distortion_results_01](distortion_results/distortion_results_01.jpg)
![distortion_results_02](distortion_results/distortion_results_02.jpg)
![distortion_results_03](distortion_results/distortion_results_03.jpg)
![distortion_results_04](distortion_results/distortion_results_04.jpg)
![distortion_results_05](distortion_results/distortion_results_05.jpg)

## 참고

- 현재 체스보드 기준 내부 코너 패턴은 `8 x 6`입니다.
- 패턴이 다른 보드를 사용할 경우 `camera_calibration.py` 실행 시 `--board_cols`, `--board_rows`를 맞게 지정하세요.
