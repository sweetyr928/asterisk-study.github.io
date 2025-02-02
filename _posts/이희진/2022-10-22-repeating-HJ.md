---
title: "이희진 복습일지"
layout: post
comments: true
categories: [이희진/복습일지]
tags: []
---

### 221011 || URI vs URL
URI는 URL를 포함하는 상위개념이라 하나 둘의 차이가 명확하게 와닿지는 않는다.  
이 둘의 명확한 구분을 위해 좀 더 상세히 살펴보면 다음과 같다.  
먼저 URI는 통합 자원 식별자(Uniform Resource Identifier)의 약자로 논리적 및 물리적 리소스를 식별하는 고유한 문자열 시퀸스다.  
그럼 URL은 무엇일까? 통합 자원 위치 탐사기(Uniform Resource Locator)로 네트워크 상에서 리소스가 어디에 있는지 알려주는 규약이다.  
요약하면 URI는 식별을 하고 URL는 위치까지 가르킨다. 그렇기 때문에 URI이더라도 위치 정보가 없다면 URL이 될 수 없으므로 'URL은 URI이다'는 성립이 되지만 'URI는 URL이다'는 성립이 되지 못한다.  

즉, 한 가지 예를 들어 설명하면 다음과 같다.  
http://asterisk.com/user?id=123  
이 경우, '?id=123(query)'의 결과에 따라 특정 자원의 결과가 다르게 나올 수 있으므로 이를 식별자라 한다. 즉, 식별자 이전까지는 URL이라 할 수 있으나 식별자가 붙은 형태는 URL이라 할 수 없고 오로지 URI라고만 할 수 있다.  
<br />

### 221016 || express 라이브러리
express.js로 서버를 여는 건 어쩌면 node.js보다 간단할 수 있다. 그럼 express 라이브러리 설치 후 실행을 시키는 건 어떤 과정을 거칠까.
```js
const express = require('express');
const app = express();

app.listen(port, function(){실행할 코드});
```   
이게 하나의 기본 양식이다. 아래의 listen()을 통해 서버를 열 수 있는데 listen()에는 총 두 개의 인자가 들어간다. 하나는 서버를 띄울 포트, 하나는 서버를 열고 실행할 코드로 완성한다면 해당 포트로 접속했을 때 사용자가 마주할 페이지를 마음대로 설정할 수 있다. 또한 여기서 멈추지 않고 서버를 띄웠을 때 서버로 오는 다양한 요청들을 처리할 수 있어야 한다. 가장 보편적인 예로 사용자가 URL을 통해 GET 요청을 보냈을 때 요청에 맞춰 페이지 응답을 보낼 수 있어야 하는 것이다.  
```js
app.get( '경로', function(req, res){
   res.send('전달인자로 받은 경로로 접속했을 때 실행할 코드);
   }
```
만약 '/books'라는 경로에 도달했을 때 다양한 책의 목록이 나오는 페이지를 띄우고 싶다면 res.send()안에 원하는 페이지를 띄우는 코드를 작성하면 된다. 이것이 기본적인 express 라이브러리를 실행하는 틀이며 다양한 활용을 통해 동적인 페이지를 구성할 수 있다.  
<br />

### 221022 || DOM(1)
DOM은 정확히 무엇일까? 브라우저 렌더링 엔진이 HTML 문서를 파싱(일련의 문자열을 token 단위로 분해해 parse tree을 생성)하여 만든 자료 구조를 DOM이라 한다. HTML 요소들(태그, 어트리뷰트 이름 및 값, 콘텐츠)은 파싱을 통해 요소 노드 객체(요소 노드, 어트리뷰트 노드, 텍스트 노드)로 변환된다.

HTML 요소 간에는 중첩 관계가 있기 때문에 이 사이엔 부모-자식 관계가 형성이 되고 이를 기반으로 비선형(하나의 자료 뒤에 여러 개의 자료가 존재함) 자료구조 중 하나인 트리 자료구조가 생성된다.

파싱을 통해 형성된 DOM의 노드 객체는 총 12개가 있으며 이 중 중요한 노드 타입은 총 4개 있다.

1. 문서 노드(Document node)  
DOM 트리의 최상위에 존재하는 루트 노드인 document 객체를 의미한다. window.document 또는 document로 참조 가능하며 이때 window 객체는 하나의 전역 객체라 모든 자바 스크립트 코드가 공유하고 window의 document 프로퍼티에 바인딩 되어 있는 하나의 document 객체를 보게 된다. 따라서, HTML 문서당 window 객체는 유일하다. 문서 노드는 앞서 말했듯 루트 노드이기 때문에 요소, 어트리뷰트, 텍스트 등 다른 노드에 접근하기 위해서는 문서 노드를 꼭 거쳐야 한다. 이러한 특징 때문에 문서 노드는 진입점 역할을 담당한다 할 수 있다. 

2. 요소 노드(Element node)  
HTML 요소를 가리키는 객체로 해당 노드는 다른 노드와 부모-자식 관계를 가질 수 있고 이 관계를 통해 구조(트리 구조)화가 가능하다. 이 때문에 요소 노드는 문서의 구조를 표현한다고 할 수 있다. 

3. 어트리뷰트 노드(attribute node)  
어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체로 해당 노드에 접근하기 위해서는 요소 노드에 먼저 접근해야 한다. 이는 어트리뷰트 노드가 오로지 요소 노드에만 연결되어 있기 때문이다. 단, 여기서 주의해야 하는 것은 해당 연결은 상위로 연결된 게 아니라 동등한 위치에서 연결된 것으로 요소 노드와 어트리뷰트 노드의 관계는 부모-자식이라 할 수 없다.  

4. 텍스트 노드(Text node)  
HTML 요소의 텍스트를 가리키는 객체로 요소 노드가 문서의 구조라면 텍스트 노드는 문서의 내용을 의미한다. 텍스트 노드는 요소 노드의 자식 노드로 접근하기 위해선 요소 노드에 먼저 접근해야 하며 텍스트 노드는 본인의 자식 노드를 가질 수 없는 리프 노드다. 즉, DOM 트리의 최종단이라 할 수 있다.  
<br />

### 221030 || DOM(2)
HTML을 자바스크립트를 사용해 동적으로 제어하기 위해선 먼저 요소 노드를 취득해야 한다. 텍스트 노드도 어트리뷰트 노드도 결국 요소 노드와 연결되어 있으므로 이는 어떤 노드를 제어하려 해도 기본적으로 요소 노드에 먼저 접근해야 함을 알 수 있다. 요소 노드를 취득하는 방법은 총 4가지로 말할 수 있다.  

1. id 이용   
* document.prototype.getElementById() 메서드 : 인수로 전달한 id 값을 갖는 하나의 요소 노드 반환하며 만약 없을 시 null 반환함
이때, HTML 요소에 id 값을 부여하면 해당 값이 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과가 발생한다.
   
2. 태그 이름 이용    
* document.prototype.getElementByTagName() 메서드 : 인수로 전달한 태그 이름을 갖는 모든 노드 요소를 HTMLCollection 객체로 반환함
이때 document 자리에 특정 요소 노드를 넣어 호출이 가능한데 이럴 경우 특정 요소 노드의 자손 노드 중에서 탐색해 반환한다.   

3. class 이용
* document.prototype.getElementsByClassName() 메서드 : 인수로 전달한 class 값을 갖는 모든 요소 노드를  HTMLCollection 객체로 반환함  

4. CSS 선택자 이용 
* document.prototype.querySelector() 메서드 : 인수로 전달한 CSS 선택자에 해당하는 하나의 요소 노드를 반환함  
* element.prototype.matches() 메서드 : 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득 가능한지에 대해 booleanr값을 반환함
<br />

### 221106 || DOM(3)
요소 노드를 취득해야 그의 자식 노드 등에 접근할 수 있다. 앞서 말했듯 자식 노드, 텍스트 노드, 어트리뷰트 노드 등에 접근하기 위해선 일단 요소 노드를 취득해야 하기 때문이다. 이번 파트에서 다룰 내용은 요소 노드 취득 후 어떻게 탐색하는가에 대한 내용이다.  

1. 자식 노드 탐색   
* Node.protptype.childNodes: 자식 노드를 전부 탐색해 Nodelist에 반환한다.
* Element.prototype.children: 자식 노드 중에서 요소 노드만 모두 탐색해 HTMLCollection에 담아 반환한다.
* Node.prototype.firstChild(lastChild): 첫 번째(마지막) 자식 노드를 반환하며 해당 노드는 텍스트 노드이거나 요소 노드이다.
* Element.protptype.first(last)ElementChild: 첫 번째(마지막) 자식 요소 노드를 반환하며 해당 노드는 요소 노드이다.   

2. 부모 노드 탐색 : Node.prototype.parentNode 프로퍼티를 이용해 탐색한다.    

3. 형제 노드 탐색   
* Node.protptype.previousSibling(nextSibling): 형제 노드 중 자신의 바로 이전(다음) 형제 노드를 탐색해 반환한다.
* Element.prototype.Previous(Next)ElementSibling: 형제 노드 중 자신의 바로 이전(다음) 형제 노드를 탐색해 반환하며 요소 노드만 반환한다.   

이렇게 탐색 후, 간혹 노드에 대한 조작이 필요한 경우가 있다. 그 중 텍스트 노드에 대한 조작이 필요할 경우 사용하는 프로퍼티는 다음과 같다.   
* nodeValue: 텍스트 노드의 nodeValue 프로퍼티에 변경하고자 하는 값을 할당하면 변경이 된다.
* textContent: nodeValue와 유사하나 HTML 마크업이 파싱되지 않아 자식 노드가 있을 경우 함부로 변경하면 자식 노드가 사라진다. 따라서 할당할 때 주의가 필요하다.
* innerText 프로퍼티 또한 텍스트 노드를 변경할 수는 있으나 CSS에 의해 비표시된 요소 노드의 텍스트를 반환하지 않는 등 CSS에 영향을 크게 받아 잘 사용하지 않는다.
<br />

### 221113 || DOM(4)
DOM 조작이란 새로운 노드를 생성해 DOM에 추가하거나 기존 노드를 삭제 또는 교체하는 것을 의미한다. 하지만 이는 성능에 영향을 미칠 수 있으므로 주의해서 다룰 필요가 있다.   
     
* innerHTML: 요소 노드의 HTML 마크업을 취득하거나 변경하는 프로퍼티로 반환값으로 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이)내에 포함된 모든 HTML 마크업을 문자열로 반환한다. 이때 textContent 프로퍼티와의 차이는 innerHTML은 HTML 마크업까지 포함한 문자열을 반환한다는 점에 있다. 해당 프로퍼티를 이용한 DOM 조작은 구현이 간단하고 직관적이라는 장점이 있으나 크로스 사이트 스크립팅 공격에 취약하다.
* Element.prototype.insertAdjacentHTML: 해당 메서드는 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입한다. 두 번째 인수로 전달한 HTML 마크업 문자열을 파싱하고 그 결과로 생성된 노드를 첫 번째 인수로 전달한 위치에 삽입해 DOM에 반영한다. 해당 메서드는 innerHTML처럼 기존 요소들을 전부 지우고 처음부터 작성하는 것이 아니라 새롭게 삽입될 요소만 파싱해 자식 요소로 추가하는 원리라 효율적이긴 하나 마찬가지로 크로스 사이트 스크립팅 공격에 취약하다.
    
위에서는 HTML 마크업 문자열을 파싱하여 노드를 생성하고 DOM에 반영한다. 이 외에도 DOM은 노드르를 직접 생성/삽입/삭제/치환하는 메서드 또한 가지고 있다.  

* Document.prototype.createElement(tag name): 요소 노드를 생성해 반환한다. 
* Document.prototype.createTextNode(value of textNode): 텍스트 노드를 생성해 반환한다. 이렇게 추가한 텍스트 노드를 요소 노드의 자식 노드로 추가하고자 할 때는 Node.prototype.appendChild(childNode)메서드를 이용해서 자식 노드 자리에 텍스트 노드를 넣는다. 또한 이를 이용해 요소 노드를 DOM에 추가할 수도 있다. 
* Node.prototype.insertBefore(newNode, childNode): 첫 번째 인수로 받은 노드를 두 번째 인수로 전달 받은 노드 앞에 삽입한다. 이때, 두 번째 인수 노드는 반드시 해당 메서드를 호출한 노드의 자식 노드여야 한다. 이러한 메서드(appendChild or insertBefore)를 이용해 노드를 이동시킬 수 있다. 
* Node.prototype.cloneNode: 노드의 사본을 생성해 반환하는 메서드로 매개변수 deep에 true를 인수로 전달하면 노드를 깊은 복사하여 모든 자손 노드가 포함된 사본을 생성하고 false를 인수로 전달하거나 생략하면 노드를 얕은 복사하여 노드 자신만의 사본을 생성한다.
* Node.prototype.replaceChild(newChild, oldChild): 자신을 호출한 노드의 자식 노드를 다른 노드로 교체하는 메서드다. 
* Node.prototype.removeChild(child): 인수로 전달한 노드를 DOM에서 삭제한다.  
<br />

### 221120 || DOM(5)
HTML 요소는 여러 개의 어트리뷰트를 가질 수 있다. 이 어트리뷰트는 요소의 동작일 제어하기 위한 추가적인 정보를 제공하는데 시작 태그 안에 '어트리뷰트 이름 = "어트리뷰트값"'과 같은 형식으로 정의한다. 글로벌 어트리뷰트(id, class, style, title 등)와 이밴트 핸들러 어트리뷰트(onclick, onchange, onblur 등)는 모든 HTML 요소에 공통적으로 사용할 수 있지만 특정 요소에서만 사용 가능한 어트리뷰트도 존재한다. input 요소에서만 사용 가능한 type, value, checked가 그것이다. 만약 요소 노드의 모든 어트리뷰트 노드를 보고 싶다면 **element.prototype.attributes** 프로퍼티를 이용해 확인할 수 있다. 그 외에도 다양한 메소드 및 프로퍼티가 존재하는데 이는 다음과 같다. 
* Element.prototype.getAttributes(어트리뷰트 이름): HTML 어트리뷰트 값 참조를 위해 사용하는 메소드다.
* Element.prototype.setAttributes(어트리뷰트 이름, 어트리뷰트값): 어트리뷰트 값을 변경할 때 사용하는 메소드다.
* Element.prototype.hasAttributes(어트리뷰트 이름): 해당 어트리뷰트의 존재 여부를 확인하는 메소드다.
* Element.prototype.removeAttributes(어트리뷰트 이름): 해당 어트리뷰트를 삭제하는 메소드다. 

요소 노드 객체에는 HTML 어트리뷰트에 대응하는 프로퍼티, DOM 프로퍼티가 존재한다. 이 DOM 프로퍼티들은 HTML 어트리뷰트 값을 초기값으로 가지고 있다. 이때 DOM 프로퍼티는 참조와 변경이 가능한 프로퍼티임을 기억해야 한다. 얼핏 생각하면 DOM 프로퍼티와 HTML 어트리뷰트가 비슷하다고 생각할 수 있으나 둘에게는 차이가 존재한다. 
HTML 어트리뷰트는 HTML 요소의 초기 상태를 지정하는 것이다. 다시 말해 HTML 어트리뷰트 값은 HTML 요소의 초기 상태를 의미하고 이는 변하지 않는다. 반대로 DOM 프로퍼티는 사용자의 입력에 의한 상태 변화에 반응하여 언제나 최신 상태를 유지한다. 요약하면 HTML 어트리뷰트는 HTML 요소의 초기 상태 값을 관리하고 DOM 프로퍼티는 사용자의 입력에 의해 변경되는 최신 상태를 관리한다. 
