# 📷 <b>Noise_Reduction_with_Autoencoder📷
### 👀프로젝트 진행에 대한 자세한 사항은 `NRwAE_progress.md`에 상세히 서술되어있습니다! 참고바랍니다.
### 👀코드와 실행 결과는 `noise_Reduction_with_autoencoder.ipynb`을 통해 바로 확인할 수 있습니다.
### 👀해당 프로젝트는 학부 3학년 1학기, `영상처리와 딥러닝` 과목에서 진행한 개인 기말 프로젝트 작품입니다.
  
## <b>프로젝트 설명
- 수업에서 오토인코더에 대해 배우게 되었는데. 이미지를 축소하여 특징들을 추려낸 후(인코더), 그 특징들을 토대로 이미지를 재구성(디코더) 할 수 있다.
  - ![image](https://user-images.githubusercontent.com/46768743/145661933-190ca233-a0b6-4335-8933-0d56689f2c1c.png)
  - `이미지 출처: https://lilianweng.github.io/lil-log/2018/08/12/from-autoencoder-to-beta-vae.html`
  - 이를 알고 원본 사진에 노이즈를 주더라도 오토인코더를 이용하면 다시 원본 사진으로 복원할 수 있겠다라는 점에서 프로젝트를 진행하게 되었다.
  
- 데이터 셋은 양이 그렇게 많지 않아도 되기 때문에 FingerNumber_classifier 프로젝트에서 사용한 데이터 셋을 가져왔다.
  - <img width="300" alt="image" src="https://user-images.githubusercontent.com/46768743/142755240-0e1a3570-e740-434a-b3e5-99a1cc9eb99d.png"> <img width="300" alt="image" src="https://user-images.githubusercontent.com/46768743/142755325-8dd0e747-12f8-4458-96fc-36a9dde59f0c.png">
  
## <b>개발 환경
- 언어: Python 3
- 환경: Google Colab
- 기간: 2021.12.03 ~ 2021.12.10

## <b>사용 방법 `(GPU를 사용할 경우)` 📖
  - CUDA 를 사용하기 위해서는 NVIDIA GPU가 필요합니다. 따라서 구글 코랩으로 진행합니다.
  - 업로드 된 `dataSet.zip` 파일과 `noise_Reduction_with_autoencoder.ipynb`파일을 다운로드 받습니다.
  - 본인의 구글 드라이브(기본경로)에 noise_reduction_with_autoencoder 폴더를 생성합니다.
  - noise_reduction_with_autoencoder폴더에 dataSet 폴더를 생성합니다.
  - dataSet폴더 안에 다운로드 받은 dataSet.zip을 압축 해제합니다.
  - 다시 `구글 코랩`으로 돌아옵니다.
  - 다운로드 받은 `noise_Reduction_with_autoencoder.ipynb`를 열어줍니다.
  - 구글 코랩의 상단부에 런타임 -> 런타임 유형 변경 -> 'None' 에서 GPU로 변경합니다.
  - <img width="446" alt="image" src="https://user-images.githubusercontent.com/46768743/142857000-db20c982-3364-477c-ba89-f8ecfffe595c.png">
  <br> - 위 그림 처럼 왼쪽 폴더 모양 아이콘을 클릭한 후 2번으로 표시된 아이콘을 누르면 마운트가 진행됩니다.
  - <img width="637" alt="image" src="https://user-images.githubusercontent.com/46768743/142857247-61e38577-3dbd-4d37-9abc-82506366e35b.png">
  <br> - 최종적으로 위와같은 이미지와 동일한 구조가 되어야 합니다.
  - 런타임이 끊길 경우 재 연결 후, 재 마운트를 해야합니다.
  - 코드를 실행합니다. (Ctrl + Enter)

  
## <b>사용 예제
- 여건이 된다면 실시간으로 손 모양을 인식하여 즉시 어느 숫자를 가리키는지 출력해주는 것이 최종 목표입니다.
  

