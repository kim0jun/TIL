GFM Basic
=================
본 문서는 kim0jun이 gfm을 공부하기위하여 작성한 문서입니다.  

##GFM이란?

GFM은 표준 Markdown(SM)에 조금더 편하게 변경한 github 버젼입니다. 
그리고 Markdown은 Plain text로 작성된 파일을 HTML로 변경해서 보여주기 위한 문법입니다.

###GFM LivePreviewer

- GFM으로 작성한 문서를 미리 볼수있는 사이트
- [바로가기](http://tmpvar.com/markdown.html)

##GFM문법

###헤더
- h1 = 또는 #
- H2 – 또는 ##
- H3 ### 
- H4 #### 
- H5 #####
- H6 ######

###줄바꿈
- 문장의 줄바꿈을 그대로 반영합니다(Enter)

###들여쓰기
> `>` 한칸들이기
>> `>>`두칸들이기

###강조
- `**`으로 감싸면 볼드표시   **볼드**
- `*`으로 감싸면 이탤릭 표시  *이탤릭*


###수정
- `~~`으로 감싸서 수정된부분을 표시
~~수정전텍스트~~ 수정된텍스트

###링크
- `[텍스트](url)` 형식으로 표시
[링크](https://github.com/kim0jun/TIL/blob/master/GFM/gfm-basic.md)

###리스트
- -,+,* 를사용하여 작성합니다.
- (기호+"공백"+"내용") 으로 작성하여야합니다.

###숫자리스트
1. 숫자+"." 를사용하여 작성합니다.
2. (숫자+"."+"공백"+"내용") 으로 작성하여야합니다.

###코드블락

- `   인라인 블락
- ``` 멀티라인 블락
- 멀티라인으로 시작할때 언어종류를 적어주면 문법에따른 하이라이트표시가된다.

```javascript
    var i:uint = 3;
```

###테이블
- `|`,`-`을 사용하여 행과 열을 표시
- 테이블 안에서도 마크다운 문법은 적용됩니다.
```
First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
```
이렇게 작성하면

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

이렇게 표시됩니다.




