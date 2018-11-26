# wai_aria

### First Rule of ARIA Use
### 규칙 1. ARIA 사용의 규칙
- If you can use a native HTML element [HTML51] or attribute with the semantics and behavior you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.

### 규칙 2. native semamtics를 변경하지 마세요

상황 1 : 개발자가 탭 역활을 하는 헤딩 태그를 마크업 하길 원한다

Don't do this
~~~html
    <h2 role="tab">heading tab</h2>
~~~

Do this
~~~html
    <div role="tab"><h2>heading tab</h2></div>
~~~

### 규칙 3. 모든 interactive ARIA controls는 keyboard와 함께 사용될 수 있어야 한다.

### 규칙 4. focusable element를 하기 위해 role="presentation" 또는 aria-hidden="true"를 사용하지 말아라

- 2가지 속성을 focusable element에 사용하는 것은 아무것도 포커싱을 할수 없는 결과를 초래할 있다

Don't do this
~~~html
    <button role"presentation">press me</button>

    <button aria-hidden="true">press me</button>
~~~

> Applying aria-hidden to a parent/ancestor of a visible interactive element will also result in the interactive element being hidden, so don't do this either:

> 상호작용하는 요소(element)인 상위 요소에 *aria-hidden* 속성을 추가하는 것은 상호작용하는 요소가 숨겨지게 될수 있습니다

Don't do this
~~~html
    <div aria-hidden="true">
        <button>press me</button>
    </div>
~~~

> If an interactive element cannot be seen or interacted with, then you can apply aria-hidden, as long as it's not focusable. For example:

> 상호작용하는 요소(element)가 보이지 않거나 상호작용하지 않는다면 당신은 *aria-hidden*을 추가할 수 있습니다. 포커스가 될 수 없기만 하면! 아래 예제 참고

~~~html
    button {opacity:0}

    <button tabindex="-1" aria-hidden="true">press me</button>
~~~

> If an interactive element is hidden using display:none or visibility:hidden (either on the element itself, or any of the element's ancestors), it won't be focusable, and it will also be removed from the accessibility tree. This makes the addition of aria-hidden="true" or explicitly setting tabindex="-1" unnecessary.

> 상호작용하는 요소(element)가 *display:none* 또는 *visibility:hidden*을 사용하여 숨김처리가 된 상태라면(그 요소 자신에게 또는 그 요소의 상위 요소에게), 그 요소는 포커스가 될 수 없다 그리고 그 요소는 *accessibility tree*에서 제거가 될 수 있다. 이러한 처리는 *aria-hidden="true"* 또는 *tabindex="-1"*의 추가를 불필요하게 만든다.

### Fifth Rule. All interactive elements must have an accessible name.
### 규칙 5. 모든 interactive 요소들은 accessible name을 가져야한다.

- An interactive element only has an accessible name when its Accessibility API accessible name (or equivalent) property has a value.

> For example, the input type=text in the code example below has a visible label 'user name' , but no accessible name:

> 예를 들면 아래 코드에 있는 *input type=text* 눈에 보이는 'user name' 텍스트를 가지고 있다. 그러나 accessible name은 존재하지 않는다

~~~html
     user name <input type="text">

        or

     <span>user name</span> <input type="text">
~~~

> In comparison, the input type=text in the code example below has a visible label 'user name' and an accessible name. This example has an accessible name because the input element is a labelable element and the label element is used correctly to associate the label text with the input.

> 비교해보면, 아래 예제 코드의 *input type=text* 눈에 보이는 'user name'그리고 accessible name을 가지고 있다. 아래 예제는 accessible name을 가진다. 왜냐하면 *input* 요소는  labelable element 그리고 *label* element는 적절하게 input 요소와 정확하게 연결이 되어있다

~~~html
<!-- Note: use of for/id or wrapping label around text
and control methods will result in an accessible name -->

<input type="text" aria-label="User Name">

or

<span id="p1">user name</span> <input type="text" aria-labelledby="p1">

~~~

> Note: The example above is for ARIA widgets. For regular HTML inputs, follow the First Rule of ARIA, and use the label element with a for attribute to associate labels with input elements.

> Note: 위의 예제들은 ARIA widgets을 위한 것입니다. HTML inputs의 요소는 label 요소를 사용하세요. input과는 *for*과 *id*를 이용해서 연결하세요



### 실무 적용해보기

아래와 같은 내용 관련해서 실무에 적용 할 수 있는 예제 및 wai-aria 속성에 관해서 명시하겠습니다

1. button
    - *button* 역할은 사용자의 동작에 반응하, 클릭할 수 있는 요소에 사용해야 합니다 혼자서 사용할 때 role="button"은 어떠한 요소(ex : <p>> <span> <div>)도 스크린 리더가 버튼으로 인식하게 할 수 있습니다. 추가로 aria-pressed 속성을 통해 토글 가능한 버튼을 만들 수 있습니다
    > 참고:  HTML 기본 버튼(<button>, <input type="button" />, <input type="submit" />, <input type="reset" />, <input type="image" />)은 모든 유저 에이전트와 보조 기술에서 지원하며 기본으로 키보드와 포커스 기능을 지원하기 때문에, 가능하면 role="button" 보다 HTML 버튼을 사용하는게 좋습니다.
    - aria-pressed="false" / aria-pressed="true" / aria-pressed="mixed"

    #### ARIA 기본 버튼
    > In the snippet below, a span element has been given the button role. Because a <span> element is used, the tabindex attribute is required to make the button focusable and part of the tab order. Note that this snippet implies that CSS styles are provided to make the <span> element look like a button and that handleBtnClick and handleBtnKeyUp are event handlers that perform the button's action when clicked and when the Space key is pressed.

    ~~~html
        <span role="button" tabindex="0" onclick="handleBtnClick()" onKeyUp="handleBtnKeyUp()">Save</span>
    ~~~

    #### ARIA 토글 버튼
    > In this snippet a native HTML button is converted to a toggle button using the aria-pressed attribute. Note that the tabindex attribute needs not to be used here because the <button> element is already focusable by default. When the button is activated, the aria-pressed value keeps on switching between true and false;

    > HTML button은 *aria-pressed* 속성을 사용해서 변환이 됩니다. *tabindex* 속성은 아래 버튼태그에서 이용할 필요가 없습니다 왜냐하면 <button> 요소는 이미 default값으로 포커스가 될 수 있기 때문입니다. *aria-pressed* value값은 true/false로 값을 계속해서 바꾸게 됩니다.

    ~~~html
        <button role="button" aria-pressed="false" onclick="handleBtnClick(event)" onKeyUp="handleBtnKeyUp(event)">Edit Mode</button>
    ~~~

    참고 url : https://developer.mozilla.org/ko/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_button_role
2. tab/pannel
    - role="tablist"
    - role="tab"
    - role="tabpanel"
    - aria-controls
    - aria-labelledby
    - tabindex
  ~~~html
    <ul class="tablist" role="tablist">
        <li id="tab1" class="tab" role="tab" aria-controls="tab-panel1">boo</li>
        <li id="tab2" class="tab" role="tab" aria-controls="tab-panel2">far</li>
        <li id="tab3" class="tab" role="tab" aria-controls="tab-panel3">baz</li>
    </ul>
    <div id="tab-panel1" class="tabpanel" role="tabpanel" aria-labelledby="tab1">
     ...
    </div>
    <div id="tab-panel2" class="tabpanel" role="tabpanel" aria-labelledby="tab2">
     ...
    </div>
    <div id="tab-panel3" class="tabpanel" role="tabpanel" aria-labelledby="tab3">
     ...
    </div>
   ~~~

   참고 url : - https://mulder21c.github.io/2018/06/04/how-to-make-accessible-tab-content/

3. popup
    - native HTML의 한계점
        - 팝업이 떴다라는 정보를 인지할 수 없다
        - 팝업 이외의 문서 정보에 접근이 된다.
        - 키보다 tab키 운용이 팝업을 벗어난다
        - 키보드 트랩 문제 (IE8 ~ 10)
    - 필요한 사항
        - 팝업이 열렸을 때 팝ㄷ업 내용 인식 가능
        - 팝업 아래의 Windows는 비활성화
        - tab키 운용이 팝업 내부에서만 순환
        - 팝업이 닫혔을 때 초점이 원래 있던 곳으로 반환
    #### how to ?
    - step 1. role = "dialog"
        - 콘텐츠 역할 정의
        > 사용자가 정보를 입력하거나 응답할 것을 요구하도록 유도하기 위해 어플리케이션의 현재 처리를 중단시키도록 설계된 어플리케이션 윈도

    ~~~html
       <div class="popup_wrap">
           <div class="popup_body" role="dialog" aria-labelledby="pop-title">
               <strong id="pop-title" class="modal_header">접근 가능한 레이어 팝업</strong>
               <div class="modal_body">
                   <p>접근 가능한 레이어 팝업이란</p>
               </div>
           </div>
       </div>
    ~~~
    - step 2.
  참고 url : - https://mulder21c.github.io/seminar/20171222/
4. nav
5. figure
6. checkbox
7. listBox
8. toolbar
9. link
10. slider
11. slider(Multi-Thumb)
12. breadcrumb

### wai-aria 속성

- aria-atomic
- aria-busy (state)
- aria-controls
- aria-current (state)- (new)
- aria-describedby
- aria-details- (new)
- aria-disabled (state)
- aria-dropeffect
- aria-errormessage- (new)
- aria-flowto
- aria-grabbed (state)
- aria-haspopup
- aria-hidden (state)
- aria-invalid (state)
- aria-keyshortcuts- (new)
- aria-label
- aria-labelledby
- aria-live
- aria-owns
- aria-relevant
- aria-roledescription- (new)

----------------------
### 참조 url
- https://w3c.github.io/using-aria/
- https://mulder21c.github.io/2018/06/04/how-to-make-accessible-tab-content/
