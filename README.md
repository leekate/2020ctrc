# 2020-ctrc-OralCancer-Classification-project

# 0. Start
  암세포 분류에 있어 병리과 의사가 암세포를 구별하는 데에 Deep Learning기술을 통한 암세포 사진 분류를 1차로 진행하고 정확도가 낮은 사진들을 추려 한번 더 확인한다면 시간과 피로를 줄일 수 있다는 연구가 있다.  Deep Learning기술을 이용해 암세포 데이터를 다룰 때 최종적으로 하고자 하는 것은 발생하는 정보의 loss를 최소화하고 전처리 과정을 거쳐 노이즈를 제거해 고해상도 의료 이미지를 훈련 영상으로 이용하여 CNN 모델을 학습시키는 것이다.
  
  기본 CNN, VGG16, ResNet과 같이 다양한 딥러닝 모델들을 통해 구강 내 상태를 분석 및 분류하고, 분류에 최적인 딥러닝 모델을 찾기 위해 각 모델 간의 성능을 비교 및 검증을 시행고자 한다. 





# 1. 데이터 원본
![원본](https://user-images.githubusercontent.com/46522501/106096465-f9cf1500-6178-11eb-8d94-f4befe72c3fd.PNG)



# 2. 데이터 증량
1) 증량 방법:
증량 후 train: validation: test=약 1: 0.4: 0.4의 비율이 되도록


2) 증량 조건:

![며흐둣샤ㅐㅜ](https://user-images.githubusercontent.com/46522501/106096948-cb9e0500-6179-11eb-8235-f22405886384.PNG)

방법(1) 일반증량:
```
rescale=1./255,
horizontal_flip=True,
vertical_flip=True,
rotation_range=40,
width_shift_range=0.2,
height_shift_range=0.2,
zoom_range=0.2
```

방법(2) 일반증량+Contrast:





# 3. train/validation/test
train: validation: test=약 1: 0.4: 0.4의 비율

cancer: 496  /  precancer: 184  /  Inflammatory: 316  /  normal: 1365

![원본](https://user-images.githubusercontent.com/46522501/106096465-f9cf1500-6178-11eb-8d94-f4befe72c3fd.PNG)





# 3-2. Histogram Equalization









# Results
사용한 두 모델 모두 50%, 60%의 성능이 나왔다. 이는 상당히 낮은 성능으로 전처리 과정이 추가로 필요해보인다. 관려 논문 읽고 적용해보자.
## 4-1. Resnet
<img width="551" alt="스크린샷 2021-01-22 오후 1 00 02" src="https://user-images.githubusercontent.com/46522501/105444736-c3ddec80-5cb1-11eb-8e67-6769d6e49170.png">

## 4-2. VGG16
<img width="620" alt="스크린샷 2021-01-22 오후 2 05 03" src="https://user-images.githubusercontent.com/46522501/105449135-1374e600-5cbb-11eb-8402-031bba3acb5c.png">








### 예상1
<img width="1150" alt="스크린샷 2021-01-25 오후 5 02 39" src="https://user-images.githubusercontent.com/46522501/105677507-4b845f00-5f2f-11eb-9fb2-7b232b86b47a.png">
Contrast로 데이터 전처리 해주고 학습을 한다면 특징이 부각되니까 더 성능이 좋아지지 않을까?

predict 결과 아래와 같은 결과가 나왔다. 전반적으로 수치가 낮으며, 특히 Precancer의 수치가 낮은 것을 확인할 수 있다.
![contrst](https://user-images.githubusercontent.com/46522501/106235507-28fb8a00-623e-11eb-8073-49d082fddf9c.PNG)


 accuracy와  loss을 확인해보아도 학습이 미흡하다는 것을 알 수 있다.
![contrast_result](https://user-images.githubusercontent.com/46522501/106235613-5d6f4600-623e-11eb-9bbd-38089340542e.png)


### 예상2
![image](https://user-images.githubusercontent.com/46522501/102291993-a5385780-3f87-11eb-957b-2086fdd33263.png)
이미지의 밝기를 일정하게 통일하고,
edge를 검출해 병변 부위를 검출해 feature로 사용한다면 성능이 좋아지지 않을까?






# 5. Final Result
Confusion Matrix:
