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
dueDate (timestamp(ms), required) - 마감일(ex. 1517081902000)
writedDate (timestamp(ms), optional) - 작성일(ex. 1517081902000)
rewardPoint (double, required) - 보상 포인트
status (enum, required) - 게시물 상태(PROCEEDING, DEADLINE...)
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
grade (enum, required) - 등급(GOLD, SILVER, BRONZE)
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
selection (boolean, required)- 피드백 채택 여부
writer (User, required) - 작성자
contents (Content List, required) - 컨텐츠
```

## Notification - Todo
```
notificationId (number, required) - 알림 ID(읽음 여부 처리를 위해)
description (string, required) -  알림 내용
actionType (string, optional) - 채택하기, 확인하기 등
creationId (number, required) - 창작물 ID(창작물로 이동하기 위해)
Todo: 읽음 여부 추가
```

## SignIn
```
accessToken (string, required) - Access Token
refreshToken (string, required) - Refresh Token(Access Token 갱신을 위해)
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
   * page (number, required) - request page number
   * cursor (number, optional) - List의 마지막 item ID
   * category (string, optional)

#### Response 200 (application/json)
* Attributes
   * status (number, required)
   * message (string, required)
   * list (Creation List, required)
   * nextPage (number, required)


### 창작물 상세조회 [GET /creations/{creationId}]
#### Request (application/json)
* Query String

#### Response 200 (application/json)
* Attributes
   * status (number, required)
   * message (string, required)
   * item (Creation, required)
   

### 창작물 추가 [POST /creations] 
#### Request (application/json)
* Attributes
   * title (string, required) - 제목
   * description (string, required) - 설명
   * category (string, required) - 카테고리
   * anonymity (boolean, required) - 작성자 프로필 익명 여부
   * rewardPoint (double, required) - 보상 포인트

#### Response 201 (application/json)
* Attributes
   * status (number, required)
   * message (string, required)
   * item (number, required) - creation ID

### 창작물 수정 [PUT /creations/{creationId}]
#### Request (application/json)
* Attributes
   * title (string, optional) - 제목
   * description (string, optional) - 설명
   * category (string, optional) - 카테고리
   * anonymity (boolean, optional) - 작성자 프로필 익명 여부
   * rewardPoint (double, optional) - 보상 포인트

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
   * Todo: 추후에 추가. page (number, required) - request page number
   * Todo: 추후에 추가. cursor (number, required) - List의 마지막 item ID

#### Response 200 (application/json)
* Attributes
   * status (number, required)
   * message (string, required)
   * list (Feedback List, required)
   * Todo: 추후에 추가. nextPage (number, required)


### 피드백 추가 [POST /creations/{creationId}/feedbacks]
#### Request (application/json)
* Attributes
   * content (string, required) - 피드백 내용
   * anonymity (boolean, required) - 작성자 프로필 익명 여부

#### Response 201 (application/json)
* Attributes


### 피드백 삭제 [DELETE /creations/{creationId}/feedbacks/{feedbackId}]
#### Request (application/json)
* Attributes
  
#### Response 200 (application/json)
* Attributes
  

---

## 유저

### 로그인 [POST /sign-in]
#### Request (application/json)
* Attributes
   * realName (string, required)
   * nickname (string, required)
   * email (string, required)
   * oauthToken (string, required)
   * oauthType (enum, required)
      * FB...

#### Response 200 (application/json)
* Attributes   
   * status (number, required)
   * message (string, required)
   * item (SignIn, required)


### 닉네임 수정 [PATCH /users/nickname]

#### Request (application/json)
* Header
   * authorization (string, required) - Bearer <Access Token>

* Attributes
   * nickname (string, required)

#### Response 200 (application/json)
* Attributes


### cloud message token 갱신 [PATCH /devices/cloud-messaging] - Todo
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
   * page (number, required) - request page number
   * cursor (number, required) - List의 마지막 item ID

#### Response 200 (application/json)
* Attributes
   * status (number, required)
   * message (string, required)
   * list (Notification List, required)
   * nextPage (number, required)
