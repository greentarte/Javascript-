## jQuery

jQuery는 DOM을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구이다. jQuery의 효용은 후속 수업을 통해서 살펴보자.

* CDN - contents delivery network

```html
<!DOCTYPE html>
<html>
<body>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
    <script>
    jQuery( document ).ready(function( $ ) {
      $('body').prepend('<h1>Hello world</h1>');
    });
    </script>
</body>
</html>
```



#### 기본문법

jQuery의 기본 문법은 단순하고 강력하다. 

![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2231.png)

$()는 jQuery의 함수이다. 이 함수의 인자로 CSS 선택자(li)를 전달하면 jQuery 객체라는 것을 리턴한다. 이 객체는 선택자에 해당하는 엘리먼트를 제어하는 다양한 메소드를 가지고 있다. 위의 그림에서 css는 선택자에 해당하는 객체들의 style에 color:red로 변경한다.

- 클래스로 찾을 경우

  $('.클래스명')

- 태그로 찾을 경우

  $('태그명')

- 아이디로 찾을 경우

  $('#아이디명')

```html
<!DOCTYPE html>
<html>
<head>
    <style>
    #demo{width:200px;float: left; margin-top:120px;}
    #execute{float: left; margin:0; font-size:0.9em;}
    #execute{padding-left: 5px}
    #execute li{list-style: none}
    #execute pre{border:1px solid gray; padding:10px;}
    </style>
</head>
<body>
<ul id="demo">
    <li class="active">HTML</li>
    <li id="active">CSS</li>
    <li class="active">JavaScript</li>
</ul>
<ul id="execute">
    <li>
        <pre>
var lis = document.getElementsByTagName('li');
for(var i=0; i&lt;lis.length; i++){
    lis[i].style.color='red';   
</pre>
        <pre>
$('li').css('color', 'red')     </pre>
        <input type="button" value="execute" onclick="$('li').css('color', 'red')" />
    </li>
    <li>
        <pre>
var lis = document.getElementsByClassName('active');
for(var i=0; i &lt; lis.length; i++){
    lis[i].style.color='red';   
}</pre>
        <pre>
$('.active').css('color', 'red')</pre>
        <input type="button" value="execute" onclick="$('.active').css('color', 'red')" />
    </li>
    <li>
        <pre>
var li = document.getElementById('active');
li.style.color='red';
li.style.textDecoration='underline';</pre>
        <pre>
$('#active').css('color', 'red').css('textDecoration', 'underline');
        </pre>
        <input type="button" value="execute" onclick="$('#active').css('color', 'red').css('textDecoration', 'underline')" />
    </li>
</ul>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
</body>
</html>
```



##### HTMLElement

```html
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="active">JavaScript</li>
</ul>
<script>
    var li = document.getElementById('active');
    console.log(li.constructor.name); // HTMLLIElement 
    var lis = document.getElementsByTagName('li');
    console.log(lis.constructor.name); // HTMLCollection
</script>
```

```html
<a id="anchor" href="http://opentutorials.org">opentutorials</a>
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="list">JavaScript</li>
</ul>
<input type="button" id="button" value="button" />
<script>
    var target = document.getElementById('list');
    console.log(target.constructor.name); // HTMLLIElement
 
    var target = document.getElementById('anchor');
    console.log(target.constructor.name); // HTMLAnchorElement
 
    var target = document.getElementById('button');
    console.log(target.constructor.name); // HTMLInputElement
 
</script>
```

이를 통해서 알 수 있는 것은 엘리먼트의 종류에 따라서 리턴되는 객체가 조금씩 다르다는 것이다. 각각의 객체의 차이점을 알아보자. 링크는 DOM의 스팩이다.

- [HTMLLIElement](http://www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/html.html#ID-74680021)
- [HTMLAnchroElement](http://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-48250443)
- [HTMLInputElement](http://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-6043025)

즉 엘리먼트 객체에 따라서 프로퍼티가 다르다는 것을 알 수 있다. 하지만 모든 엘리먼트들은 HTMLElement를 상속 받고 있다. 

모든 엘리먼트는 HTMLElement의 자식이다. 따라서 HTMLElement의 프로퍼티를 똑같이 가지고 있다. 동시에 엘리먼트의 성격에 따라서 자신만의 프로퍼티를 가지고 있는데 이것은 엘리먼트의 성격에 따라서 달라진다. HTMLElement는 [Element](https://developer.mozilla.org/en-US/docs/Web/API/element)의 자식이고 Element는 [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)의 자식이다. Node는 Object의 자식이다. 이러한 관계를 DOM Tree라고 한다.

![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2234.png)

 이러한 관계를 이해하지 못하면 필요한 API를 찾아내는 것이 어렵거나 몹시 혼란스러울 것이다. 다행인 것은 jQuery와 같은 라이브러리를 이용한다면 이러한 관계를 몰라도 된다. 혹시 이해가 안된다고 너무 상심하지 말자.



##### HTMLCollection

HTMLCollection은 리턴 결과가 복수인 경우에 사용하게 되는 객체다. 유사배열로 배열과 비슷한 사용방법을 가지고 있지만 배열은 아니다. 

[HTMLCollection](http://www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/html.html#ID-75708506)

HTMLCollection의 목록은 실시간으로 변경된다. 아래 코드를 보자.

```html
<!DOCTYPE html>
<html>
<body>
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="active">JavaScript</li>
</ul>
<script>
console.group('before'); //console.log를 그룹으로 요약해서 보여줌
var lis = document.getElementsByTagName('li');
for(var i = 0; i < lis.length; i++){
    console.log(lis[i]);
}
console.groupEnd();
console.group('after');
lis[1].parentNode.removeChild(lis[1]);
for(var i = 0; i < lis.length; i++){
    console.log(lis[i]);
}
console.groupEnd();
</script>
</body>
</html>
```

결과

![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2232.png)





##### jQuery 객체특성

jQuery 객체란?

> jQuery 함수의 리턴값으로 jQuery 함수를 이용해서 선택한 엘리먼트들에 대해서 처리할 작업을 프로퍼티로 가지고 있는 객체다.

암시적 반복

> jQuery 객체의 가장 중요한 특성은 암시적인 반복을 수행한다는 것이다. DOM과 다르게 jQuery 객체의 메소드를 실행하면 선택된 엘리먼트 전체에 대해서 동시에 작업이 처리된다.
>
> 암시적 반복은 값을 설정할 때만 동작한다. 값을 가져올 때는 선택된 엘리먼트 중 첫번째에 대한 값만을 반환한다. 이에 대한 내용은 아래에서 살펴본다.



체이닝

> chainig이란 선택된 엘리먼트에 대해서 연속적으로 작업을 처리할 수 있는 방법이다. 



jQuery 객체에는 조회된 엘리먼트가 담겨 있다. jQuery 객체는 일종의 유사배열의 형태로 조회된 엘리먼트를 가지고 있기 때문에 배열처럼 사용해서 엘리먼트를 가져올 수 있다.

```html
<ul>
    <li>html</li>
    <li>css</li>
    <li>JavaScript</li>
</ul>
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    console.log($('li').length);
    console.log($('li')[0]);
    var li = $('li');
    for(var i=0; i<li.length; i++){
        console.log(li[i]);
    }
    //li태그의 색깔을 빨간색으로 변경
   for(var i=0; i<li.length; i++){
    $(li[i]).css('color', 'red');
	}
</script>
```

한가지 주의할 것은 li[i]의 값은 해당 엘리먼트에 대한 jQuery 객체가 아니라 DOM 객체라는 것이다. 따라서 jQuery의 기능을 이용해서 이 객체를 제어하려면 jQuery 함수를 이용해야 한다. 

map은 jQuery 객체의 엘리먼트를 하나씩 순회한다. 이 때 첫번째 인자로 전달된 함수가 호출되는데 첫번째 인자로 엘리먼트의 인덱스, 두번째 인자로 엘리먼트 객체(DOM)이 전달된다. [참고](https://api.jquery.com/map/) 

```html
<ul>
    <li>html</li>
    <li>css</li>
    <li>JavaScript</li>
</ul>
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    var li = $('li');
    li.map(function(index, elem){
        console.log(index, elem);
        $(elem).css('color', 'red');
    })
</script>
```



##### jQuery 객체 API

제어할 대상을 선택한 후에는 대상에 대한 연산을 해야한다. .css와 .attr은 jQuery 객체가 가지고 있는 메소드 중의 하나인데, jQuery는 그 외에도 많은 API를 제공하고 있다. 이에 대한 내용은 jQuery API를 참고하자.

[https://api.jquery.com](https://api.jquery.com/)