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

## 6. 2021.12.09
- 오류 폭탄,, 해결하는데 많은 시간이 들었음
- 일단 단순 이미지 재 구성은 완벽하게 동작, (UNet, MSELoss함수, Adam함수 사용)
- 그런데 노이즈 제거 결과가 매우 이상함 
- ![image](https://user-images.githubusercontent.com/46768743/145506513-77f3d78d-8817-40ca-ac4d-2547c3f48ae8.png)

  - Loss는 낮은데 왜,, 설마 MSELoss로 측정하면 안되나..?

## 7. 2021.12.10
- 노이즈 제거 결과가 이상한 이유 예측
  - 1. transpose가 잘못 진행되어 이미지가 90도 전환됨. 그럼 당연히 이상하게나오지!
    - ![image](https://user-images.githubusercontent.com/46768743/145506553-96b478c9-a5b0-4cfa-b850-219b83b6b383.png)
      - 이 사진을 보고 파악완료. 다 죽었어

    - ![image](https://user-images.githubusercontent.com/46768743/145506659-72ad2c0a-2908-49f1-9223-e50c9d534f5d.png)
      - 50 에포크 노이즈 제거 결과. 오? 학습을 더 진행해봐야겠다.

    - ![image](https://user-images.githubusercontent.com/46768743/145507147-26a564e5-9004-4730-b840-c25a7d23dd4b.png)
      - 200 에포크 노이즈 제거 결과. 빨간 부분의 노이즈가 작아지긴 하는데 완벽하지않다. 학습횟수의 문제가 아닌듯.
  - 2. MSELoss에 대한 고찰 
    - MSELoss는 각 픽셀마다의 거리를 측정하기 때문에 사진 처럼 다른 부분을 최대한 비스무리하게 만드는 대신 오차들을 한곳에 모으는 현상이 발생할 수도 있을 듯.  
    - Loss Functions for Image Restoration with Neural Networks (IEEE TMI 2016)
    - 위 논문을 참고하니 SSIM Loss가 노이즈를 제거하는데 가장 좋은 로스지표가 된다는 것을 확인하였다. 사실 SSIM LOSS와 L1 Loss를 혼합했을때 가장 높은 퍼포먼스를 보인다고 하지만 일단 SSIMLoss만 적용시켜본다.
  - 3. SSIM 적용 실패, 오류를 해결하지 못했다.
  - 4. 에포크 수 대폭 늘림
    - 기존 100에포크에서 2000에포크만큼 학습을 시켰더니 완벽하지는 않지만 노이즈가 거의 사라졌다.
      - 100 에포크 시 Loss: 0.028, 2000에포크 시 Loss: 0.0045
      - 결과는 ipynb 파일을 참고하자. 
    - 사실 특정 부분의 노이즈(ex. 낙서 등)이 아니라 모든 픽셀에 대해 노이즈를 줬기 때문에 컴퓨터 입장에서는 매우 큰 이미지 손실일 것이다.
  - 5. 프로그램 완성.
