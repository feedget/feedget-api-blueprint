# Model

## Category - Todo
```
name (string, required) - 카테고리 이름
```

## Creation
```
creationId (number, required) - 창작물 ID
title (string, required) - 제목
description (string, required) - 설명
dueDate (timestamp, required) - 마감일
writedDate (timestamp, optional) - 작성일
rewardPoint (number, required) - 보상 포인트
status (string, required) - 게시물 상태(PROCEEDING, DEADLINE...)
anonymity (boolean, required)- 작성자 프로필 익명 여부
feedbackCount (number, required) - 피드백 갯수
wroteFeedback (boolean, optional) - 피드백 작성 여부
writer (User, required) - 작성자
contents (Content List, required) - 컨텐츠
```

## User
```
userId (string, required) - 유저 ID
nickname (string, required) - 닉네임
grade (string, required) - 등급(GOLD, SILVER, BRONZE)
```

## Content
```
contentId (number, optional) - 컨텐츠 ID
url (string, required) - URL
```

## Feedback - Todo
```
feedbackId (number, required) -  피드백 ID
description (string, required) - 피드백 내용
anonymity (boolean, required)- 작성자 프로필 익명 여부
writer (User, required) - 작성자
contents (Content List, required) - 컨텐츠
// Todo: 채택 여부 추가
```

## Notification - Todo
```
notificationId (number, required) - 알림 ID(읽음 여부 처리를 위해)
description (string, required) -  알림 내용
actionType (string, optional) - 채택하기, 확인하기 등
creationId (number, required) - 창작물 ID(창작물로 이동하기 위해)
Todo: 읽음 여부 추가
```


<br/>
---

# API

## 카테고리 - Todo

### 카테고리 리스트 [GET /categories] 
#### Request (application/json)
* Attributes

#### Response 200 (application/json)
* Attributes
   * categories(Category List, required)


---

## 창작물

### 창작물 리스트 [GET /creations] 
#### Request (application/json)
* Query String
   * page (number, required)
   * cursor (number, optional)
   * category (string, optional)

#### Response 200 (application/json)
* Attributes
   * creations (Creation List, required)
   * nextPage (number, required)


### 창작물 상세조회 [GET /creations/{creationId}]
#### Request (application/json)
* Query String

#### Response 200 (application/json)
* Attributes
   * creation (Creation, required)


### 창작물 추가 [POST /creations] 
#### Request (application/json)
* Attributes
   * title (string, required) - 제목
   * description (string, required) - 설명
   * category (string, required) - 카테고리
   * anonymity (boolean, required) - 작성자 프로필 익명 여부
   * rewardPoint (number, required) - 보상 포인트

#### Response 201 (application/json)
* Attributes


### 창작물 수정 [PUT /creations/{creationId}]
#### Request (application/json)
* Attributes
   * title (string, optional) - 제목
   * description (string, optional) - 설명
   * category (string, optional) - 카테고리
   * anonymity (boolean, optional) - 작성자 프로필 익명 여부
   * rewardPoint (number, optional) - 보상 포인트

#### Response 200 (application/json)
* Attributes


### 창작물 삭제 [DELETE /creations/{creationId}]
#### Request (application/json)
* Query String

#### Response 200 (application/json)
* Attributes


---

## 창작물의 컨텐츠

### 창작물의 컨텐츠 추가 [POST creations/{creationId}/contents]
#### Request (multipart/form-data)
* Attributes
   * type (string, required) - 컨텐츠 타입
      * IMAGE
   * files (MultipartFile List, required) 

#### Response 201 (application/json)
* Attributes


### 창작물의 컨텐츠 삭제 [DELETE /creations/{creationId}/contents]

#### Request (application/json)
* Query String
   * contentId (string List, required)

#### Response 200 (application/json)
* Attributes


---


## 피드백

### 피드백 리스트 [GET /creations/{creationId}/feedbacks]
#### Request (application/json)
* Query String
   * page (number, required)
   * cursor (number, )required

#### Response 200 (application/json)
* Attributes
   * feedbacks (Feedback List, required)
   * nextPage (number, required)


### 피드백 추가 [POST /creations/{creationId}/feedbacks]
#### Request (application/json)
* Attributes
   * description (string, required) - 피드백 내용
   * anonymity (boolean, required) - 작성자 프로필 익명 여부

#### Response 201 (application/json)
* Attributes


### 피드백 삭제 [DELETE /creations/{creationId}/feedbacks/{feedbackId}]
#### Request (application/json)
* Attributes
  
#### Response 200 (application/json)
* Attributes
  

---

## 유저 - Todo

### 로그인 [POST /users/register]
#### Request (application/json)
* Attributes
   * oAuthToken (string, required)
   * oAuthType (string, required)
      * FB...  
Todo: 필요한 정보 추가

#### Response 200 (application/json)
* Attributes
   * accessToken (string, required)


### 닉네임 수정 [PATCH /users/nickname]

#### Request (application/json)
* Attributes
   * nickname (string, required)

#### Response 200 (application/json)
* Attributes
   * accessToken (string, required)


### cloud message token 갱신 [PATCH /devices/cloud-messaging]
#### Request (application/json)
* Attributes
   * cloudMsgRegToken (string, required)

#### Response 200 (application/json)
* Attributes


---

## 알림

### 알림 리스트 [GET /notifications]
#### Request (application/json)
* Query String
   * page (number, required)
   * cursor (number, required)

#### Response 200 (application/json)
* Attributes
   * notifications (Notification List, required)
   * nextPage (number, required)
