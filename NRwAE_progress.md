# Object_blur-out progress

## 1. 2021.12.01
- 오토인코더 이론 복습

## 2. 2021.12.03
- 주제 변경
  - Object_Blur-out: 오토인코더를 이용한 물체감지 후 모자이크화 --> Noise_Reduction_with_Autoencoder: 오토인코더를 이용한 이미지 노이즈 제거
  - 물체감지를 오토인코더로 구현하는 방법을 떠올리지 못함.
  - 오토인코더 모델 구현 (latent size: 7*7)

## 3. 2021.12.06
- 데이터셋을 FingerNumber_Classifier프로젝트의 데이터셋을 그대로 가져옴
- 오토인코더를 이용해 학습 구현
  - 학습 결과 이미지화
- latent size: 7 * 7 --> 14 * 14로 변경
  - 데이터 손실이 너무 컸음
- 정상적으로 학습 완료

## 4. 2021.12.07
- 이미지 노이즈 추가.
  - ```python
    train_noisy.append(sample_Image[i].cpu().numpy() + noise_force * np.random.normal(loc=0.0, scale=1.0, size=sample_Image[i].shape))
    ```
    - noise_force : 0.2
- learning_rate: 2e-4로 변경, 무난히 학습이 잘되는 수치
- 노이즈 제거 모델 구현중.. 구현이 완료되면 추가기능을 제공해볼 

## 5. 2021.12.08
- 기존 선형 오토인코더 에서 `UNet`으로 변환, 노이즈 제거 후 성능 향상을 위함
  - 참고: https://www.youtube.com/watch?v=sSxdQq9CCx0&t=329s
- transform 재구성
