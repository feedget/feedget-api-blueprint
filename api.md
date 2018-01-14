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
feedbackCount (number, required) - 피드백 갯수
writer (User, required) - 작성자
contents (Content List, required) - 컨텐츠
wroteFeedback (boolean, required) - 피드백 작성 여부
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
writer (User, required) - 작성자
contents (Content List, required) - 컨텐츠
// Todo: 채택 여부 추가
```

## Notification - Todo
```
description (string, required) - 설명
// Todo: click interaction에 따른 추가 정보 ex. creationId
```


<br/><br/>
---

# API

## 카테고리 - Todo

### 카테고리 리스트 [GET /categories] 
* Request (application/json)

* Response 200 (application/json)
```
{
    categories(Category, required)
}
```

## 창작물
