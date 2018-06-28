#### 자바스크립트 사용 설명서

chrome console에서 연습(ctrl + L clear)

1. 자료형

   1. 숫자

   2. 문자 => 'string' of "string"

   3. null => 아무것도 없다는 값이 값으로 들어 있음

   4. undefined => 값이 할당되어 있지 않음 ( == 값만 비교, === 값과 자료형까지 비교 )

   5. boolean => true,false

   6. 객체(Object) => {}   //hash(ruby)

      1. 키와 값을 쌍으로 가짐

      2. var o = {key:value}

      3. 함수를 값으로 가질 수 있음

      4. Method, property

      5. value에 함수가 들어있을 경우, method

      6.  그 외의 값은 property

      7. 배열(array) => []

         1.  유용한 methods

            - pop(마지막값 가져오고 배열에서 빠짐)
            - shift(첫번째 값을 가져옴)
            - unshift(i) i값을 배열 맨 앞에 삽입함
            - push( 마지막에 삽입)
            - sort(오름차순 정렬)
            -  sort().reverse() 내림차순 정렬
            - reverse()  순서만 반대로 정렬
            - indexOf(i)  배열안에 i값의 위치를 알려줌
            - forEach 배열값을 1개 씩 출력함

         2. 더 유용한 메소드

            - .filter(조건) 

              배열의 모든 값에 함수를 적용 시킨 후, true인 값만 새로운 배열에 삽입해 반환한다.

               true or false형태의 결과가 나오는 조건을 넣어주면 true면 남기고   false면 안남긴다 

            - ```javascript
              var arr = [-1,3,-5,7,-9]
              function getPositive(x) {
                  return x>2; 
              }
              var arr2 = arr.filter(getPositive) ==> (2) [3, 7]
              ```

            - .map(함수) => 배열의 모든 값에 함수를 적용 시킨 후, 새로운 배열을 반환한다.

2. 함수

   1. 함수 선언식

      ```javascript
      function sum(x,y){
          return x+y;
      }
      ```

   2. 함수 표현식

      ```javascript
      var sum = function(x,y) {
          return x+y;
      }
      ```

   3. 차이점

      ```javascript
      //함수 선언식(실행 코드보다 아래에 선언되도 함수가 동작함(페이지를 불러올때 함수 우선 실행)
      // 실제 작성 코드
      sum(1,2);
      function sum(x,y){
          console.log(x+y);
      }
      ```

      ```javascript
      // 위의 코드가 실행되는 순서
      function sum(x,y){
          console.log(x+y);
      }
      sum(1,2);
      
      ```

      ```javascript
      // 함수 표현식(변수의 경우 변수 선언만 되기 때문에 실행이 안됨)
      // 실제 작성 코드
      sum(1,2);
      var sum = function(x,y){
          console.log(x+y);
      }
      ```

      ```javascript
      // 위의 코드가 실행되는 순서
      var sum;
      sum(1,2);
      sum = function(x,y){
          console.log(x+y);
      }
      ```

   4. 함수의 다양한 용도(인자, 리턴값)

      ```javascript
      var arr = [1,2,3,4,5];
      var double = function(x) {return x*2};
      //var arr2 = arr.map(double);
      var arr2 = map(double, arr);
      function map(func, arr){
        var new_arr = [];
        for (element of arr) {
              new_arr.push(func(element));
        }
          return new_arr;
      }
      
      var positive = function(x) {return x > 0};
      //positive(1)  => true
      //positive(-1) => false
      var arr = [-1,3,-5,7,-9];
      
      //var arr2 = arr.filter(positive);
      var arr2 = filter(positive,arr); // arr2 = > 3,7
      function filter(func, arr){
          var new_arr = [];
          for(element of arr){
              if(func(element)){
                  new_arr.push(element);
              }
          }
          return new_arr;
      }
      
      //2. 함수 리턴
      function func1(){
          return function func2(){
              console.log("I'm inner function")
          }
      }
      var test = func1(); //test == func2
      test();
      ```

   5. 함수의 인자 사용법

      ```javascript
      function sum(a,b){
          console.log(a+b);
      }
      sum(1) // => 들어오지 않은 값은 undefined
      //console.log(1+undefined);
      // => NaN
      sum(1,2,3) // => 더 들어오는 인자도 arguments로 사용 가능
      //arguments = [1,2,3,]
      
      function sum(a,b){
          var total = 0;
          for (element of arguments){
              total += element;
          }
          console.log(total);
      }
      sum(1,2,3,4,5) // => 15
      
      function multiple(){
          var total = 1;
          for (element of arguments){
              total *= element;
          }
          console.log(total);
      }
      multiple(1,2,3,4,5) //=> 120
      ```

3. 변수 스코프

   ```javascript
   var i = 0; //전역변수
   function changeI() {
       i = 10;
       console.log(i);
   }
   changeI(); //10 
   console.log(i) //10
   
   var i =0;
   function changeI(){
       var i = 10; //지역변수
       console.log(i)
   }
   changeI(); //10
   console.log(i) //0
   ```

   ```javascript
   //정적 유효범위
   var i = 0;
   function a(){
       var i = 10;
       b(); // 함수 호출시 변수 참조 X
   }
   function b(){
       console.log(i); //함수 선언시 변수 참조 O
   }
   a() //콘솔에 나오는 값은? => 0 
   
   i = 10;
   a() //콘솔에 나오는 값은? => 10
   
   //함수 내 지역 변수 참조하는 방법 => 함수 내에서 함수를 선언해준다.
   var i = 0;
   function a() {
       var i = 10;
       function b(){
           console.log(i); // var i = 10;
       }
       b();
   }
   a(); // 콘솔에 나오는 값은? => 10
   
   //클로저
   var i = 0;
   function a(){
       var i = 10;
       return function b(){
           console.log(i);
       }
   }
   var closure = a();
   closure() //콘솔에 나오는 값은? => 10
   ```

4. Hoisting(끌어 올림)

   ```javascript
   // 실제코드
   console.log(1);
   var i = 0;
   
   func();
   function func(){
       console.log("func!!");
   }
   ```

   ```javascript
   //실행될 때 코드
   function func(){
       console.log("func1!");
   }
   var i;
   
   console.log(i); //콘솔에 찍히는 값은? undefined
   i=0;
   func(); //콘솔에 찍히는 값은? func!!
   ```

   ```javascript
   //2번째 예시 실제코드
   var i = 0 ;
   function func2() {
       console.log(i);
       var i = 10;
   }
   func2() //콘솔에 찍히는 값은?? => undefined
   ```

   ```javascript
   //실행될 때 코드
   var i = 0;
   function func2(){
       var i;
       console.log(i);
       i = 10;
   }
   func2() // 콘솔에 찍히는 값은?? => undefined
   ```

   ```javascript
   // 3번째 예시
   // 실제 코드
   var language = 'Java';
   function checkScript(script){
       if (script){
           var language = "ruby";
           console.log(language);
       } else {
           console.log(language);
       }
   }
   checkScript(true); // 콘솔에 찍히는 값은? ruby
   checkScript(false); // 콘솔에 찍히는 값은? undefined
   ```

   ```javascript
   // 실행 코드
   var language = 'Java';
   function checkScript(script){
       var language;
       if (script){
            language = "ruby";
           console.log(language);
       } else {
           console.log(language);
       }
   }
   checkScript(true); // 콘솔에 찍히는 값은? ruby
   checkScript(false); // 콘솔에 찍히는 값은? undefined
   ```

   ```javascript
   // 3번째 예시 해결책1 : 전역변수를 참조하게 한다.
   var language = 'Java';
   function checkScript(script){
       if (script){
            language = "ruby";
           console.log(language);
       } else {
           console.log(language);
       }
   }
   checkScript(true); // 콘솔에 찍히는 값은? ruby
   checkScript(false); // 콘솔에 찍히는 값은? Java
   ```

   ```javascript
   // 3번째 예시 해결책2 : 변수를 let으로 선언한다.
   var language = 'Java';
   function checkScript(script){
       if (script){ //let 시작
            let language = "ruby";  //let을 사용하면 괄호안을 벗어나지 않는다.
           console.log(language); //let 끝
       } else {
           console.log(language);  //전역변수를 출력함
       }
   }
   checkScript(true); // 콘솔에 찍히는 값은? ruby
   checkScript(false); // 콘솔에 찍히는 값은? Java
   ```

5.  this

   ```javascript
   var globalThis = null;
   
   //1. 함ㅁ수에서 사용되는 this
   function this1(){
       globalThis = this; // window => 현재 코드가 실행되는 브라우저의 창
   }
   this1();
   globalThis
   
   //2. method에서 사용되는 this => this는 메소드를 사용하는 객체
   var o = {
       p1: 'property1',
       m1: this1
   };
   o.m1();
   globalThis
   
   //2-1. 예시2
   var o2 = {
       prop: 1,
       method: function(){
           console.log(this.prop1);
       }
   };
   
   o2.method(); //콘솔에 찍히는 값은? 1 = this.prop1 == o2.prop1
   
   //3. 생성자에서 사용되는 this
   function Person(name){ //생성자 함수, 클래스와 같은 역할을 함
       this.name = name; // this는 생성된 객체를 의미함
   }
   var p1 = new Person("john"); //this == p1
   p1.name // => "john"
   
   //예시 3-1.
   var globalThis = null;
   function this1(){
       globalThis = this; //window => 현재 코드가 시행되는 브라우저의 창
   }
   var o1 = new this1();
   globalThis // => o1 this를 받는 대상이 없으면 window가 호출됨
   ```

6. this와 관련된 methods( call, apply, bind)

   ```javascript
   function Person(name){
       this.name = name;
   }
   var p1 = new Person("john");
   var p2 = {};
   Person.call(p2, "john"); //call(this, arguments)
   p2 // {name: "john"}
   //----------------------------------------------------
   
   function Person(name, age){
       this.name = name;
       this.age = age;
   }
   var p3 = {};
   Person.call(p3, "john",33)
   p3 // {name: "john", age: 33}
   
   //----------------------------------------------------
   
   var globalThis = null;
   
   function testFunc(){
       globalThis = this;
   }
   
   var testVar = 20;
   testFunc.call(testVar);
   globalThis // = > Number {20}
   
   //2. apply
   // call이랑 동일함. arguments를 넣는 방식만 다름.
   Person.call(p3, "john", 33) // ,로 구분해서 인자들을 전해줌.
   Person.apply(p3, ["john",33]) // 배열 안에 몽땅 넣어서 전해줌.
   
   
   //3. bind(this에 해당하는 대상) & 함수가 실행되진 않음.
   //this에 해당하는 대상을 지정만 해주는 역할
   var globalThis = null;
   function testFunc(a,b){
       globalThis = this;
       console.log(a+b);
   }
   var bindedFunc = testFunc.bind(20);
   
   
   ```

7. 클로저 (외부 함수의 변수들에 접근 가능한 내부 함수)

   ```javascript
   //version 1
   var arr=[];
   for (var i=0; i<10; i++){
       arr[i]=function outer(i){
           	function inner(){
           		return i * 20;    
           	}
       		return inner;    
       }(i);
   }
   
   //version 2
   var arr=[];
   function outer(i){
       return function outer(i){
           return function inner(){
               return i * 20;
           }
       }
       for (var i=0; i<10; i++){
           arr[i] = outer(i);
       }
   }
   
   //출력 코드
   for( j in arr){
       console.log(arr[j]()); //0,20,40,60, ...200
   }
   
   /* for문 상세 예시
   var i = 0;
   arr[i] = function() { return i * 20}; // i == 0 => 10
   i +=1
   arr[i] = function() { return i * 20};
   i +=1
   arr[i] = function() { return i * 20};
   i +=1
   arr[i] = function() { return i * 20};
   i +=1
   arr[i] = function() { return i * 20};
   i +=1
   arr[i] = function() { return i * 20}; // i == 10
   /////////////////
   console.log(arr[0]) // 200
   console.log(arr[1]) // 200
   console.log(arr[2]) // 200
   */
   
   //클로저(외부 함수 안에 있는 내부 함수)
   //내부 함수는 외부함수의 변수들에 접근 가능.
   //외부함수는 내부함수의 변수들에 접근 불가.
   var i = 0;
   function outer(){
   //    var i = 10;
   //    var j = 20;
   //    var k = 30;
       function inner(){
           var innerVar = 100;
           console.log(i);
           console.log(j);
           console.log(k);
       }
       //console.log(innerVar); 접근 불가
       return inner;
   }
   var closure = outer(); //변수 closure에는 함수 inner가 들어가 있음, inner함수에서는 함수 outer의 변수인 i,j,k에 접근이 가능함.
   closure() //콘솔에 나오는 값은? => 10,20,30
   
   var closure = function outer(i){
       return function inner(){
           console.log(i);
       }
   }(1);
   ```

8. prototype(상속, 클래스 변수를 정의하는 것과 같은 역할)

   ```javascript
   function Person(){
       this.purpose = "happiness";
   }
   function Adult(){
       this.age = "higher than 20"
   }
   function Child(){
       this.age = "lower than 20"
   }
   
   Adult.prototype = new Person();  //Audlt가 Person에게 상속받음
   Child.prototype = new Person();  //Child가 Person에게 상속받음
   var a1 = new Adult();
   a1.purpose;
   
   var c1 = new Child();
   c1.purpose;
   
   var p1 = new Person();
   var p2 = new Person();
   
   Person.prototype.name = "john";
   Person.prototype.printName = function(){
       console.log(this.name)
   };
   
   //1. prototype을 통해 상속을 구현할 수 있다.
   Child.prototype = new Parent();
   var c1 = new Child();
   var p1 = new Person();
   c1.purpose == p1.purpose;
   
   //2. prototype을 통해 메소드와 프로퍼티를 객체 간에 공유할 수 있다.
   Child.prototype.name="john"
   ```

   