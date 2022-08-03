---
title: 'ReactNative의 핵심 컴포넌트'
subtitle: 'map으로 프로젝트를 진행하던 도중, 마주한 혁신적인 컴포넌트에 대햐서'
date: 2022-05-27 20:40:00
category: 'ReactNative'
---

![](https://velog.velcdn.com/images/willy4202/post/b8f48c95-e559-4a31-88f1-baad96026709/image.png)

리액트 네이티브는 스크롤이 되는 div와 안되는 div로 나눠진다.

이를 `ScrollView`와 `View`라고 한다

스크롤할 수 있는 컨테이너로 여러개의 컴포넌트를 담아서 스크롤할 수 있는 역할을 한다.

그리고 세로나 가로로 스크롤할 수 있고 둘중에 하나만 스크롤할 수 있다.

스크롤뷰라는 코어 컴포넌트 안에 텍스트, 이미지를 배치하고 렌더링 하면
요소의 수 만큼 스크롤이 가능하게 된다.

테이블 뷰, 리스트 뷰와 다른 차이점은 서로 다른 요소를 담을 수 있다.

ios의 경우에는 하나만 담아두어도 줌 처리를 할 수 있다.

하나의 주의할 점이 있다.

스크롤뷰는 렌더링시 화면에 보이지 않는 부분에 대해서도 미리 렌더링 처리를 한다.

리스트 뷰 같은 경우에는 화면에 보일때만 렌더링하는 방식이지만

스크롤 뷰는 화면에 미리 다 그려놓는 편이라

속도 같은 면에서 차이가 생길 수 있겠다.

뿐만 아니라, 화면이 그려지고 나서 작동하는 Hook을 걸어둔다면 그런 것들이 실행된다는 뜻이고, 화면의 리소스도 차지하게 된다.

함부로 쓰게 된다면 리소스를 낭비할 수 있게 되는 것이다.

### ScrollView 요약

ScrollView는 다른 컴포넌트나 뷰를 담는 공간이다.

각각의 요소는 서로 다른 형태여도 된다.

Ios에서는 한 요소만 담아두고 내용을 확대해서 보는데도 활용할 수 있다.

주의 // 화면에 보이지 않는 영역들도 렌더링이 됨

---

## 리스트 뷰

여러개의 리스트 컴포넌트를 보여줄때 일반적으로 `FlatList`와 `ScetionList`를 많이 사용한다.

`FlatList` : 일종의 `map`을 가능하게 해주는 컴포넌트로, 배열을 첫번째 요소에 `data`를 받아 `renerItem`을 통해 그려줄 수 있다.

```Jsx
    <View style={styles.container}>
      <FlatList
        data={[
          {key: 'Devin'},
          {key: 'Dan'},
          {key: 'Dominic'},
          {key: 'Jackson'},
          {key: 'James'},
          {key: 'Joel'},
          {key: 'John'},
          {key: 'Jillian'},
          {key: 'Jimmy'},
          {key: 'Julie'},
        ]}
        renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
      />
    </View>
```

![](https://velog.velcdn.com/images/willy4202/post/95dff97b-893e-42f5-b6cd-a66e54303aa0/image.png)

`scrollView`와 다르게 보이는 부분에서만 렌더링이 처리된다는 특징이 있다.

`SectionList` : Map을 가능하게 하지만, 조금 더 나아간다. 섹션으로 그룹을 지어 각 섹션에 헤더를 줄 수 있는 방식이다. 아이템을 렌더링하고, 이후엔 구분을 줄 수 있는 아주 편리한 컴포넌트다.

`setions`, `rednerItem`, `renderSectionHeader`, `keyExtractor`를 받아서 사용할 수 있다.

```jsx
<View style={styles.container}>
  <SectionList
    sections={[
      { title: 'D', data: ['Devin', 'Dan', 'Dominic'] },
      { title: 'J', data: ['Jackson', 'James', 'Jillian', 'Jimmy', 'Joel', 'John', 'Julie'] },
    ]}
    renderItem={({ item }) => <Text style={styles.item}>{item}</Text>}
    renderSectionHeader={({ section }) => <Text style={styles.sectionHeader}>{section.title}</Text>}
    keyExtractor={(item, index) => index}
  />
</View>
```

![](https://velog.velcdn.com/images/willy4202/post/2ef8f512-4c5f-479b-8f1c-0df54fcc62d7/image.png)

컴포넌트 자체에 아이템을 반복하게 해줄 수 있는 기능이 있다니,,
그저 혁신이다.

만약 데이터를 받아서 리스트로 뿌려줄 때 일일이 map 함수를 작성하지 말고
이렇게 List를 활용해보자.
