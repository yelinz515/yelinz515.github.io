---
title: "Cmarket Hooks"
date: "2022-08-31"
author: 김예린
categories: codestates blog
---

## Side Effect

> 함수의 입력 외에도 함수의 결과에 영향을 미치는 요인

ex) 네트워크 요청 (백엔드 API 요청)

<br>



## Cmarket Hooks

지금까지 배운 React Router, React Hooks를 이용해 과제를 해보았다. 어려웠던 부분, 부족한 부분, 느낀점에 대해 얘기해보려 한다.

### App.js
---
```js
function App() {
  const [items, setItems] = useState(initialState.items);
  const [cartItems, setCartItems] = useState(initialState.cartItems);

  return (
    <Router>
      <Nav cartItems={cartItems}/>
      <Routes>
        <Route path="/" element={<ItemListContainer cartItems={cartItems} setCartItems={setCartItems} items={items} />} />
        <Route
          path="/shoppingcart"
          element={<ShoppingCart setCartItems={setCartItems} cartItems={cartItems} items={items} />}
        />
      </Routes>
      <img
        id="logo_foot"
        src={`${process.env.PUBLIC_URL}/codestates-logo.png`}
        alt="logo_foot"
      />
    </Router>
  );
}

export default App;
```

<br>

### 어려웠던 내용 🤢

### ItemListContainer.js
---

```js
function ItemListContainer({ items, cartItems, setCartItems }) {

  const handleClick = (itemId) => { 
    const found = cartItems.filter(item => item.itemId === itemId)[0];
    // 장바구니에 새로 추가
    if(found === undefined){
      setCartItems([...cartItems, {itemId, quantity : 1}])
      console.log(setCartItems)
    }
  }
  return (
        {items.map((item, idx) => <Item item={item} key={idx} handleClick={handleClick} />)}
  );
}
```

`cartItems.itemId`와 `itemId`가 같으면 found이다. [0]을 해준 이유는 기존에 장바구니에 없었다면 undefined였을 것이고, 있었다면 undefined가 아니기 때문이다. 그래서 조건이 undefined라면 수량을 1로해서 새로 추가하는 것이다.

<br>

### ShoppingCart.js
---
```js
export default function ShoppingCart({ items, cartItems, setCartItems }) {
  const [checkedItems, setCheckedItems] = useState(cartItems.map((el) => el.itemId))

  const handleQuantityChange = (quantity, itemId) => {
    setCartItems(cartItems.map((item) => itemId === item.itemId ? {"itemId":itemId, "quantity":quantity} : item))
  }

  const handleDelete = (itemId) => {
    setCheckedItems(checkedItems.filter((el) => el !== itemId))
    setCartItems(cartItems.filter((el) => el.itemId !== itemId))
  }

  return (...)
}
```

`handleQuantityChange`는 장바구니에 있는 수량 버튼을 눌러 수량을 추가하거나 삭제할 수 있다.

`'handleDelete'`는 `cartItems.itemId`과 `itemId`가 일치하지 않은 아이템을 장바구니에 남겨놓는다.

<br>

### 부족한 내용 🧐
---

장바구니에 있던 아이템을 다시 장바구니에 넣으면 기존에 있던 수량에 추가되는 기능을 넣어보면 좋을 것 같다.

<br>

## 느낀점 🤠
---

오늘은 과제를 해결해 나갈 수 있게 지시해주는 TODO가 없어서 어려웠다. TODO의 소중함을 깨닫는 시간이었다. 다시 풀어보고 더 공부해보겠습니다.