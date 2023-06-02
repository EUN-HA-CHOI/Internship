### innerHTML , innerText, textContent 차이점.    

```javascript 
<body>
<div id='my_div'>
안녕하세요? 만나서 반가워요.
<span style='display:none'>숨겨진 텍스트</span>
</div>
<input type='button'
value='innerHTML'
onclick='getInnerHTML()'/>
<input type='button'
value='innerText'
onclick='getInnerText()'/>
<input type='button'
value='textContent'
onclick='getTextContent()'/>
</body>
```

```javascript
function getInnerHTML() {
const element = document.getElementById('my_div');
alert(element.innerHTML);
}
function getInnerText() {
const element = document.getElementById('my_div');
alert(element.innerText);
}
function getTextContent() {
const element = document.getElementById('my_div');
alert(element.textContent);
}
```

### innerHTML
해당 Element 의 HTML , XML 을 읽어오거나, 설정할 수 있다. 위 예제에서 'innerHTML' 버튼을 클릭하면,
div 안에 있는 HTML 전체 내용을 가져오는 것을 확인 할 수 있다.
![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/9664d985-bd2a-4f54-b42b-4dceb2506598)

### innerText
해당 Element 내에서 사용자에게 ‘보여지는’ 텍스트 값을 읽어온다. 위 예제에서 'innerText' 버튼을 클릭하면, 아래와 같은 텍스트를 가져
온다.

![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/d582c595-0337-4b4e-8db1-5754a8d1ba24)

원래 div 를 보면 안녕하세요? 만나서 반가워요. 가 입력되어 있지만, 브라우저가 사용자에게 이 내용을 보여줄 때는, 연속되는 공백
을 무시하고 하나의 공백만 처리하여 안녕하세요? 만나서 반가워요. 라고 보여준다.

또한, 예제의 div 는 'display:none' 으로 정의된 텍스트를 포함하고 있다. 이는 브라우저에 보여주지 않는다.
이처럼 innerText 는 사용자에게 보여지는 텍스트를 가져온다.  

### textContent
<script> 나 <style> 태그와 상관없이 해상 노드가 가지고 있는 텍스트 값을 그대로 읽는다.
안녕하세요? 만나서 반가워요. 의 연속된 공백이 그대로 표현된 것을 확인 할 수 있다.
  ![image](https://github.com/EUN-HA-CHOI/Internship/assets/97012561/504eeb29-719e-43d8-a6f0-c553cca93e7d)

또한, ‘display:none' 스타일이 적용된 '숨겨진 텍스트 ’ 문자열도 그대로 출력 되는 것을 확인 할 수 있다.
일반 text 값을 가지고 올때는 세 가지 속성에 별 차이가 없지만, element 가 가지고 있는 컨텐츠의 내용에 따라서 차이가 나는 것을 확인 할
수 있다.
