---
emoji: 📔
title: "React Custom Component"
date: "2022-08-30"
author: 김예린
categories: codestates blog
---

Styled-Component, useRef를 이용해 과제를 해보았다. 어려웠던 부분, 부족한 부분, 느낀점에 대해 얘기해보려 한다.



## 어려웠던 내용 🤢


### Tag.js
---

```js
  const initialTags = ['CodeStates', 'kimcoding'];

  const [tags, setTags] = useState(initialTags);
  const removeTags = (indexToRemove) => {
    tags.splice(indexToRemove, 1);
    setTags([...tags])
```

`removeTags`에서는 태그를 삭제하기 위해 `splice`를 이용해 태그를 하나씩 삭제하고, `setTags`에 전개연산자를 이용해 `tags`의 좌항에서 명시적으로 할당되지 않은 나머지 배열 값들을 나타낸다.

```js
  const addTags = (event) => {

    // - 아무것도 입력하지 않은 채 Enter 키 입력시 메소드 실행하지 말기
    if(event.key !== 'Enter') return;
    const val = event.target.value;
    if(!val) return;
    // - 이미 입력되어 있는 태그인지 검사하여 이미 있는 태그 아니거나 마우것도 입력하지 않았다면 추가하기
    if(!tags.includes(val) && val !== ""){
      setTags(prev => [...prev, val])
      // - 태그가 추가되면 input 창 비우기
      event.target.value = ''
    }
  };
```
`addTags`에서는 tags 배열에 새로운 태그를 추가해야 한다. 주석을 참고하면 된다.

<br>

### Autocomplete.js(수정)
---

```js
const deselectedOptions = [
  'rustic',
  'antique',
  'vinyl',
  'vintage',
  'refurbished',
  '신품',
  '빈티지',
  '중고A급',
  '중고B급',
  '골동품'
];

(...)

export const Autocomplete = () => {
  const [hasText, setHasText] = useState(false);
  const [inputValue, setInputValue] = useState('');
  const [options, setOptions] = useState(deselectedOptions);
  const [selected, setSelected] = useState(-1);

  useEffect(() => {
    if (inputValue === '') {
      setHasText(false);
    }
  }, [inputValue]);

  const handleInputChange = (event) => {
    const { value } = event.target;

    // input에 텍스트가 있는지 없는지 확인하는 코드
    value ? setHasText(true) : setHasText(false);

    // updateText
    setInputValue(value);

    // dropdown을 위한 기능
    const filterRegex = new RegExp(value, 'i'); // new RegExp 하면, RegExp 객체가 생성(텍스트를 판별할 때 사용)
    const resultOptions = deselectedOptions.filter((option) =>
      option.match(filterRegex)
    );
    setOptions(resultOptions);
  };

  const handleDropDownClick = (clickedOption) => {
    setInputValue(clickedOption);
    const resultOptions = deselectedOptions.filter(
      (option) => option === clickedOption
    );
    setOptions(resultOptions);
  };

  const handleDeleteButtonClick = () => {
    setInputValue('');
  };

 // 키보드로 DropDown 선택
  const handleKeyUp = (event) => {
    if (hasText) {
      if (event.code === 'ArrowDown' && options.length - 1 > selected) {
        setSelected(selected + 1);
      }
      if (event.code === 'ArrowUp' && selected >= 0) {
        setSelected(selected - 1);
      }
      if (event.code === 'Enter' && selected >= 0) {
        handleDropDownClick(options[selected]);
        setSelected(-1);
      }
    }
  };

  return (
    <div className='autocomplete-wrapper' onKeyUp={handleKeyUp}>
      <InputContainer hasText={hasText}>
        <input
          type='text'
          className='autocomplete-input'
          onChange={handleInputChange}
          value={inputValue}
        />
        <div className='delete-button' onClick={handleDeleteButtonClick}>
          &times;
        </div>
      </InputContainer>
      {hasText ? (
        <DropDown
          options={options}
          handleDropDownClick={handleDropDownClick}
          selected={selected}
        />
      ) : null}
    </div>
  );
};

export const DropDown = ({ options, handleDropDownClick, selected }) => {
  return (
    <DropDownContainer>
      {options.map((option, idx) => (
        <li
          key={idx}
          onClick={() => handleDropDownClick(option)}
          className={selected === idx ? 'selected' : ''}
        >
          {option}
        </li>
      ))}
    </DropDownContainer>
  );
};
```

~다시 테스트해보고 설명하도록 하겠습니다.~

<br>

### ClickToEdit.js
---

```js
 const handleBlur = () => {
    setEditMode(false);
    handleValueChange(newValue);
  };

  (...)

    return (
    <InputBox>
      {isEditMode ? (
        <InputEdit
          type='text'
          value={newValue}
          ref={inputEl}
          onBlur = {handleBlur}
          onChange = {handleInputChange}
        />
      ) : (
        <span
        onClick ={handleClick}
        >{newValue}</span>
      )}
    </InputBox>
  );
}
```

`onBlur = {handleBlur}`가 뭘까?

> onblur : 포커스가 해지될 때 이벤트 설정

`<span>`을 클릭했을 때, 우리는 `<InputEdit>`에서 글을 수정할 수 있다. 다음 `<span>`을 클릭해 글을 적으려고 했을 때, 다시 `<span>`으로 돌아가야한다. 이때 `onBlur` 이벤트를 통해 설정할 수 있다. 

`onBlur` 이벤트를 쓰지 않으면, 그대로 `<InputEdit>`에 머물러 있게 된다.

<br>

## 부족한 내용 🧐

### Modal.js
---

```js
export const ModalBackdrop = styled.div`
  // Modal이 떴을 때의 배경을 깔아주는 CSS를 구현
  background-color: rgba(0, 0, 0, 0.3);
  left:0; right:0; top:0; bottom:0;
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
`;

export const ModalView = styled.div.attrs((props) => ({
  // attrs 메소드를 이용해서 아래와 같이 div 엘리먼트에 속성을 추가 가능
  role: 'dialog',
}))`
  // Modal창 CSS를 구현
  border: 1px solid;
  width: 300px;
  height: 100px;
  background-color: white;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  > button {
    background: none;
    border: none;
    color: black;
    font-size: 1rem;
    margin-top: -30px;
  }
`;

export const Modal = () => {
  const [isOpen, setIsOpen] = useState(false);

  const openModalHandler = () => {
    setIsOpen(!isOpen);
  };

    return (

        (...)

        {isOpen ? <ModalBackdrop onClick={openModalHandler}>
          <ModalView onClick = {e => e.stopPropagation()}>
            <button onClick={openModalHandler}>x</button>
                모달 창
          </ModalView>
        </ModalBackdrop>: ""}
    )
}
```

`<ModalBackdrop>`과 `<button>`을 클릭하면 `<ModalView>`가 나타난다. 여기서 중요한 점은  `<ModalView>`를 닫을 때  `<ModalBackdrop>`과 `<button>`을 클릭해야 닫혀야 하는데 `<ModalView>`를 눌러도 닫힌다. 

부모 엘리먼트에게도 이벤트가 전파되지 않기 위해 `e.stopPropagation`을 사용한다.

> **e.stopPropagation**는 이벤트가 상위 엘리먼트에 전달되지 않게 막아 준다.

`e.stopPropagation`를 기억해두자!

<br>

### Toggle.js
---

```js
const ToggleContainer = styled.div`
  position: relative;
  margin-top: 8rem;
  left: 47%;
  cursor: pointer;

  > .toggle-container {
    width: 50px;
    height: 24px;
    border-radius: 30px;
    background-color: #8b8b8b;
    // TODO : .toggle--checked 클래스가 활성화 되었을 경우의 CSS를 구현합니다.
    &.toggle--checked {
      background-color: blue;
      transition: 0.5s;
    }
  }

  > .toggle-circle {
    position: absolute;
    top: 1px;
    left: 1px;
    width: 22px;
    height: 22px;
    border-radius: 50%;
    background-color: #ffffff;
    transition: 0.5s;
    // TODO : .toggle--checked 클래스가 활성화 되었을 경우의 CSS를 구현합니다.
    &.toggle--checked {
      left: 27px;
      transition: 0.5s;
    }
  }
`;
```

Styled-Components 부분에서 `> .toggle-circle`, `&.toggle--checked` 사용한 점이다.

`> .toggle-circle`는 ToggleContainer안에 있는 toggle-circle를 의미한다. className = "toggle-circle" 이다.


`&.toggle--checked` 클래스의 코드를 각각 `.toggle-container`, `.toggle-circle`와 연결해준다. className = "toggle--checked toggle-container" 라고 쓸 수 있다.


> 엠퍼샌드(&)를 사용하여 해당 컴포넌트를 재참조한다.

**엠퍼샌드(&)** 를 잘 활용하면 글로벌로 걸려있는 스타일과 충돌이 일어날 수 있을 때에도 유용하게 처리할 수 있다는 장점이 있다.



<br>

### Tab.js
---

```js
  .submenu {
    width : calc(100% / 3);
    text-align: center;
    padding: 10px;
  }
```

> `calc()`는 괄호 안의 식을 계산한 결과를 속성값으로 사용하게 해주는 함수이다. 

예를 들어, 3개의 버튼이 있다면 공평하게 세 부분으로 나누고 싶을 것이다. 그럼 width: 33%를 해야하는가? 

그럴 필요 없다. 위 코드처럼 `calc()`함수를 이용해서 해결하면 된다.

<br>



## 느낀점 🤠
---

페어와 함께 과제를 수행했다. 혼자서 과제를 다시 이해하고 싶어서 처음부터 과제를 다시 풀었다. Styled-Components 라이브러리로 HTML + JS + CSS까지 묶어서 하나의 JS파일 안에서 컴포넌트 단위로 개발할 수 있어서 너무 편했고, Styled-Components 사용법에 대해 더 자세히 알 수 있어서 좋았다.