---
title: "Cmarket Redux"
date: "2022-09-02"
author: 김예린
categories: codestates blog
---

## Cmarket Redux


Redux의 원리와 구조, 즉 설계하면서 어려웠던 부분, 부족한 부분, 느낀점에 대해 얘기해보려 한다.

<br>

## 어려웠던 내용 🤢


### ShoppingCart.js
---

```js

(...)

  const { cartItems, items } = state
  const [checkedItems, setCheckedItems] = useState(cartItems.map((el) => el.itemId))
  const handleCheckChange = (checked, id) => {

      if(checked){
        // 눌렀을 때 itemid가 같으면 체크가 선택되라
        setCheckedItems(checkedItems.concat(id))
      }
      else {
        // 눌렀을 때 체크가 해제되면 빈 배열로 만들어라
        let off = checkedItems.filter((el) => el !== id)
        setCheckedItems(off)
      }

  };

  const handleAllCheck = (checked) => {
    // 체크박스 전체 선택
    // 눌렀을 때 itemid가 같으면 체크가 선택되라
    if(checked){
      setCheckedItems(cartItems.map((el) => el.itemId))
    }
    else {
      // 눌렀을 때 체크가 해제되면 빈 배열로 만들어라
      setCheckedItems([])
    }
  };

(...)  
```

`handleCheckChange`와 `handleAllCheck`는 `usestate`를 이용해 풀 수 있었다. 이 부분은 과제할 때 작성되어 있어서 대충 보고 그냥 넘어간 것 같다. 그래서 페어와 함께 다시 지우고 작성해보았다. 어떤식으로 장바구니 안 체크박스가 해제되고 선택되는지 알 수 있는 시간이었다. ~(이 페어분과 다음에 같이 만나서 다른 과제를 다시 풀어보기로 했다ㅋㅋㅋ)~

<br>

## 부족한 내용 🧐

### itemReducer.js
---

```js

(...)

    case SET_QUANTITY:
      let idx = state.cartItems.findIndex(el => el.itemId === action.payload.itemId)
      let newArr  = state.cartItems.map((el, index) => {
        if(idx === index){
          return {itemId: action.payload.itemId, quantity: action.payload.quantity}
        }
        else {
          return el
        }
      })
      return Object.assign({}, state, {
        cartItems: newArr
      })

(...)
```

if문에서 불변성을 지키는 코드를 작성하려고 하니까 많이 어려웠다. 결국 레퍼런스를 참고했지만, 나중에 스스로 작성할 수 있도록 더 열심히 공부해야겠다.. 

<br>

## 느낀점 🤠
---
이틀 간 주어진 과제였고, 첫 날에 과제를 완성해서 제출했다. todo를 통해 풀긴 했지만, 아직 이해가 가지 않는 코드들이 많았다. 그래서 페어와 함께 다시 작성했던 코드를 지우고.. 지워서 작성할 수 있는 건 싹 다 지웠다.

다음 날, 다시 풀어보면서 Redux의 소중함을 다시 알게 되었고, 장바구니 안 체크박스나 주문 합계 등 어떻게 쓰이고 있는지 알 수 있어서 좋은 시간이었다.