DOM ( Document Object Model)

> 웹페이지의 내용을 제어한다. window의 프로퍼티인 document 프로퍼터에 할당된 Document 객체가 이러한 작업을 담당한다.  Document 객체의 프로퍼티는 문서 내의 주요 엘리먼트에 접근할 수 있는 객체를 제공한다.

```html
<!DOCTYPE html>
<html>
<body>
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <img src="https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/course/94.png" />
    <script>
        // body 객체
        console.log(document.body);
        // 이미지 객체들의 리스트
        console.log(document.images);
        // 또한 특정한 엘러먼트의 객체를 획득할 수 있는 메소드도 제공한다. 
        // body 객체
        console.log(document.getElementsByTagName('body')[0]);
        // 이미지 객체들의 리스트
        console.log(document.getElementsByTagName('body'));
    </script>
</body>
</html>
```





BOM( Browser Object Model)

> 웹페이지의 내용을 제외한 브라우저의 각종 요소들을 객체화시킨 것이다. 전역객체 Window의 프로퍼티에 속한 객체들이 이에 속한다. 
>
> navigator, screen, location, frames

```html
<!DOCTYPE html>
<html>
<body>
    <input type="button" onclick="alert(window.location)" value="alert(window.location)" />
    <input type="button" onclick="window.open('bom.html')" value="window.open('bom.html')" />
</body>
</html>
```





JavaScript ( Core ) 

Object, Array, Function