---
layout: archive
title:  "[React Native] - Redux"
categories:
    - React Native
tags:
    - React Native
gallery:
  - url: /assets/images/redux_1.png
    image_path: /assets/images/redux_1.png
    alt: "placeholder image 1"
    title: "Image 1 title caption"
  - url: /assets/images/redux_2.png
    image_path: /assets/images/redux_2.png
    alt: "placeholder image 2"
    title: "Image 2 title caption"
  - url: /assets/images/redux_3.png
    image_path: /assets/images/redux_3.png
    alt: "placeholder image 3"
    title: "Image 3 title caption"
---

Redux

---

<br>
<strong>Redux 란?</strong>

>애플리케이션 로직이 잘 구성되어 있고 앱이 예상대로 작동하는지 확인하는 상태 관리용 라이브러리 <br>
>Redux를 사용하면 언제, 어디서, 왜, 어떻게 애플리케이션 상태가 업데이트되는지에 관한 애플리케이션 코드를 쉽게 이해할 수 있다.

---

<strong>구성요소</strong>

Redux는 아래 5가지 핵심 파트로 구성되어있다.

- action
- reducer
- store
- dispatch
- selector

---

<strong>Action</strong>

- Action은 type field 와 optional payload 가 있는 Javascript 객체이다.
- 상태에 어떤 변화가 필요하게 될 때 액션을 발생시킨다.

```javascript
const addTaskAction = {
    type: 'task/taskAdded',
    payload: 'Laundry'
}
```
---
<strong>Action Creator</strong>

- Action Creator는 action 객체를 만들고 반환 해주는 함수이다.
- Action Creator 함수는 나중에 컴포넌트에서 더욱 쉽게 액션을 발생시키기 위함
- 보통 함수 앞에 export 키워드를 붙여서 다른 파일에서 불러와서 사용

```javascript
const addTask = text => {
  return {
    type: 'task/taskAdded',
    payload: text
  }
}
```

---

<strong>Reducer</strong>

- 현재 상태와 전달 받은 액션을 참고하여 새로운 상태를 만들어서 반환하는 함수이다.

- 기존 상태를 수정할 수 없고 기존 상태를 복사하여 복사된 값을 변경한다.

- 순수 함수여야 한다.


```javascript
const initialState = { value: 0 }
 
function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === 'counter/increment') {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1
    }
  }
  // otherwise return the existing state unchanged
  return state
}
```

---

<strong>Store</strong>

- Redux 에서는 한 애플리케이션 당 하나의 스토어를 만든다. 

- 스토어 안에는 현재의 앱 상태와 리듀서가 들어있고 추가적으로 몇가지 내장 함수가 있다.

- configureStore 함수에 Reducer를 전달하여 저장소의 초기 상태를 만든다.

```javascript
import { configureStore } from '@reduxjs/toolkit'
 
const store = configureStore({ reducer: counterReducer })
 
console.log(store.getState())
```

---

<strong>Dispatch</strong>
- dispatch()는 store의 내장함수 중 하나이며 action을 파라미터로 전달한다.
  
- addTask() action creator를 사용하여 task/taskAdded action을 생성하고 이를 dispatch() 메서드에 전달한다.

```javascript
store.dispatch(addTask('pick up laundry'))
```

---

<strong>Selector</strong>

- Selector는 store 데이터를 읽는데 사용된다.

---

### 예제

###### 1. Home.js, Subjects.js 생성

```javascript
//Home.js
 
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
 
class Home extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Home!</Text>
      </View>
    )
  }  
}

const styles = StyleSheet.create({
  container : {
      flex: 1,
      justifyContent: "center",
      alignItems: "center"
  }
});
 
// ...
export default Home;
```

```js
//Subjects.js 
 
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
 
class Subjects extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Subjects!</Text>
      </View>
    )
  }  
}

const styles = StyleSheet.create({
  container : {
      flex: 1,
      justifyContent: "center",
      alignItems: "center"
  }
});
 
// ...
export default Subjects;
```

---

###### 2. 네비게이션 설정

- 두 개의 화면을 이어줄 네비게이션이 필요하다.
- stack navigator를 사용하면 각 새화면이 스택 맨 위에 배치되도록 하는 화면 전환이 가능하다.

1) navigation 설치

```zsh
npm install @react-navigation/native
```

2) 종속 패키지 설치
```zsh
npm install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

3) App.js 수정

```Stack.Navigator```,```Stack.Screen``` 를 ```NavigatonContainer``` 컴포넌트로 감싼다.

```js
import 'react-native-gesture-handler';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import Home from './Home.js';
import Subjects from './Subjects';
//...

const Stack = createNativeStackNavigator();

class App extends React.Component {
  render() {
    return (
      <NavigationContainer>
        <Stack.Navigator>
          <Stack.Screen
            name="Home"
            component={Home}
          />
          <Stack.Screen
            name="Subjects"
            component={Subjects}
          />
        </Stack.Navigator>
      </NavigationContainer>
    )
  }
}
export default App;
```

---

### Redux 설치
```zsh
npm install redux react-redux
```  

Redux 앱은 두 가지 조건을 따른다. 

- state는 특정 시점에서 앱의 state를 완전히 설명해줘야한다.
- UI는 앱의 state에 따라 렌더링 된다.
  
예를 들어 사용자가 버튼을 클릭하면 state가 업데이트되고 UI는 state를 기반으로 변경 사항을 렌더링한다.

---

### Reducer 생성

- Reducer는 모든 시점에서 subject의 state를 유지하는 역할을 한다.

1) SubjectsReducer.js 생성

```javascript
import { combineReducers } from 'redux';
 
const INITIAL_STATE = {
  current: [],
  all_subjects: [
    'Literature',
    'Speech',
    'Writing',
    'Algebra',
    'Geometry',
    'Statistics',
    'Chemisrty',
    'Biology',
    'Physics',
    'Economics',
    'Geography',
    'History',
  ],
};
 
const subjectsReducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
    default:
      return state
  }
};
 
export default combineReducers({
  subjects: subjectsReducer
});
```

- 모든 커리큘림 과목으로 ```INITIAL_STATE``` 변수를 만들고 ```subjectsReducers```를 ```subjects```라는 속성으로 export 한다.

- ```subejcts reducers```는 어떠한 action에 반응하지않는다. 

- 따라서 state는 변화하지 않는다.
<br>

---

### Action 생성

action은 ```type```과 ```payload```(optional)로 구성되어있다.

<details>
<summary>payload 란?</summary>
<div markdown="1">
- payload는 redux앱에서 액션에 대해서 추가 정보를 제공한다.<br>
- 보통 key와 value로 이루어져 있고 JS 타입 어떤 것이든 쓸 수 있다. ( array, object ...)

</div>
</details>

1) SubjectsActions.js 파일 생성

```javascript
export const addSubject = subjectsIndex => (
  {
    type: 'SELECT_SUBJECT',
    payload: subjectsIndex,
  }
);
```

2) SubjectsReducer.js 파일 수정

- action에 대하여 반응하는 reducer로 로직 수정
  
```javascript
// ...
 
const subjectsReducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
    case 'SELECT_SUBJECT':
      
      // copy the state 
      const { current,  all_subjects,} = state;
 
      //remove a subject from the all_subjects array
      const addedSubject = all_subjects.splice(action.payload, 1);
 
      // put subject in current array
      current.push(addedSubject);
 
      // update the redux state to reflect the change
      const newState = { current, all_subjects };
       
      //return new state
      return newState;
 
    default:
      return state
  }
};
 
// ...
```

---

### App에 Reducer추가하기

1) app.js 수정

- createStore() 메소드를 사용해서 새로운 store를 생성한다.
- ```<Provider>``` 컴포넌트를 통해 다른 컴포넌트에서 store 사용이 가능하게 한다.

```javascript
import 'react-native-gesture-handler';
import React from 'react';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import { StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import subjectsReducer from './SubjectsReducer';
import Home from './Home';
import Subjects from './Subjects';
 
// ... . rest of the code
 
const store = createStore(subjectsReducer);
 
class App extends React.Component {
  // ...
 
  render() {
    return (
      <Provider store={store}>
        <NavigationContainer>
          //.. rest of the code
        </NavigationContainer>
      </Provider>
    )
  }
}
```
---

### 컴포넌트에 Redux 추가하기

- ```connect()``` 함수로 컴포넌트에서 state 데이터를 사용가능하게 해준다.
- ```connect()``` 함수를 사용하려면, store에 있는 state를 props로 매핑해주는 ```mapStateToProps``` 함수를 만들어야한다.

```javascript
//Home.js
import React from 'react';
import { connect } from 'react-redux';
import { StyleSheet, Text, View, Button } from 'react-native';
 
class Home extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>You have { this.props.subjects.current.length } subjects.</Text>
        <Button
          title="Select more subjects"
          onPress={() =>
            this.props.navigation.navigate('Subjects')
          }
        />
      </View>
    );
  }
}
 
 
const mapStateToProps = (state) => {
  const { subjects } = state
  return { subjects }
};
 
export default connect(mapStateToProps)(Home);
```

```javascript
//Subjects.js
import React from 'react';
import { connect } from 'react-redux';
import { StyleSheet, Text, View, Button } from 'react-native';
 
class Subjects extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>My Subjects!</Text>
        />
      </View>
    );
  }
}
 
//...
 
const mapStateToProps = (state) => {
  const { subjects } = state
  return { subjects }
};
 
export default connect(mapStateToProps)(Subjects);
```

---

### store에 액션 전송

- ```dispatch``` 함수를 통하여 스토어에 액션을 전달한다.

```javascript
import React from 'react';
import { connect } from 'react-redux';
import { StyleSheet, Text, View, Button } from 'react-native';
import { addSubject } from './SubjectsActions';

class Subjects extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Select Subjects Below!</Text>
        {
          this.props.subjects.all_subjects.map((subject, index) => (
            <Button
              key={ subject }
              title={ `Add ${ subject }` }
              onPress={() =>
                this.props.dispatch(addSubject(index))
              }
            />
          ))
        }
        <Button
          title="Back to home"
          onPress={() =>
            this.props.navigation.navigate('Home')
          }
        />
      </View>      
    )
  }
}
```
---

### 완성된 화면


{% include gallery %}

---

###### 참고

[완성코드](https://github.com/dbwnsgur741/redux_tutorial)<br>
[using-redux-in-a-react-native-app](https://code.tutsplus.com/tutorials/using-redux-in-a-react-native-app--cms-36001)<br>


