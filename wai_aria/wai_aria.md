# wai_aria

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

   ```
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
   ```
3. popup
4. nav
5. figure
6. checkbox

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

