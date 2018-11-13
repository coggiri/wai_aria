# wai_aria

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

2가지 속성을 focusable element에 사용하는 것은 아무것도 포커싱을 할수 없는 결과를 초래할 있다

Don't do this
~~~html
    <button role"presentation">press me</button>

    <button aria-hidden="true">press me</button>
~~~



### 실무 적용해보기

아래와 같은 내용 관련해서 실무에 적용 할 수 있는 예제 및 wai-aria 속성에 관해서 명시하겠습니다

1. button
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

3. popup
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

