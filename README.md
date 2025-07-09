# 13일차

## 1. openCV 내의 MOG2 배경차분법 예제
[예제 코드](0709_python_MOG2_차량감지.ipynb)

- 실무에서 전처리할때 일부 사용됨
- 교수님이 주신 예제 코드에서 필터링을 하나씩 추가해나감.
- 아래 사진들은 Colab에서 동영상을 일일히 업로드하지 않으려 쓰는 방법
![KakaoTalk_20250709_085709399](https://github.com/user-attachments/assets/f92eb082-8fbc-4135-8a66-f0045d5063df)
![KakaoTalk_20250709_085808412](https://github.com/user-attachments/assets/6e5c5a55-e79a-4092-819a-6492445a0498)
![KakaoTalk_20250709_085751043](https://github.com/user-attachments/assets/9e196505-67c4-4cee-b610-44af5918df5b)
![KakaoTalk_20250709_085728404](https://github.com/user-attachments/assets/503c3f6c-a3b3-45bc-ada6-e7e7b998e57a)

## 2. 어제 0708에 했던 신호등 검출 문제 코드 추가 분석
[김영빈님 코드](https://github.com/audalsgh/20250708/blob/main/0708_openCV_%EC%8B%A0%ED%98%B8%EB%93%B1%EA%B2%80%EC%B6%9C_%EA%B9%80%EC%98%81%EB%B9%88%EB%8B%98%EC%BD%94%EB%93%9C.ipynb)<br>

![image](https://github.com/user-attachments/assets/6096ea2e-cb46-488b-b009-114fb62d3bf8)

초록색 반투명 영역을 ROI영역으로 지정하신듯, 신호등 검출 영역을 좁게 지정해줌으로써 노이즈를 줄였다.<br>
그러나, 실제 검출영역으로 쓰이고 있진 않다.<br>
detect_traffic_light_canny() 함수내에서 새로 정의된 영역만 검출에 사용중이다.
```python
# 위치 체크
        x, y, w, h = cv2.boundingRect(contour)
        # if y > image_height * 0.9:  # 기존은 하단 10%는 제외했었다. (더 관대하게)
        # 새로운 영역 (상단 15% 제거, 하단 25% 제거)  추가 수정11시51분

        center_y = y + h // 2
        if (center_y >= image_height * 0.45 and center_y <= image_height * 0.60):
```
