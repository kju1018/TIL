#  Android - 알림

오늘은 안드로이드 푸시 알림을 공부해 보았다. 어떻게 보면 기초 내용이지만 공부를 미루다 오늘 공부하게 되었다.

1. 간단한 레이아웃을 작성

   ![알림 - 1](https://user-images.githubusercontent.com/61860897/104737478-a11a7800-5787-11eb-87c0-49c83ffceca7.png)

2. Notification 생성

![알림 - 2](https://user-images.githubusercontent.com/61860897/104737485-a2e43b80-5787-11eb-84df-acbcf1c7c6e4.png)

오레오 이후부터는 체널ID를 따로 적어줘야 한다.

아이콘, 내용, 제목을 적어준다.

3.

![알림 - 3](https://user-images.githubusercontent.com/61860897/104737487-a4156880-5787-11eb-9546-1d4e992cc94b.png)

Intent와 PendingIntent를 이용하여 Notification에 지정해준다.

4.

![알림 - 4](https://user-images.githubusercontent.com/61860897/104737493-a4adff00-5787-11eb-8877-08097d5ef804.png)

큰 이미지 적용, 색상 변경, 알림음 등을 알림을 커스텀 할 수 있다.

5. 

![알림 - 5](https://user-images.githubusercontent.com/61860897/104737495-a5df2c00-5787-11eb-9f39-6a6616f1070e.png)

오레오 이상 NotificationManager에 채널 Id를 등록해야 하기 위한 코드이다.

6. 결과

![알림 - 6](https://user-images.githubusercontent.com/61860897/104737498-a7105900-5787-11eb-889f-160a386e5d62.png)