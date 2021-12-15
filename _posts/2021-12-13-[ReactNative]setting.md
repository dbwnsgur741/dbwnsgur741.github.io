---
layout: archive
title:  "[React Native] - 환경세팅"
categories:
    - React Native
tags:
    - React Native
---

[React Native] MAC(M1)개발 환경 세팅

---
<br>
<strong>CLI 로 React Native 시작하기</strong>
<br>

```
node (v) : 14.18.1
npm (v) : 7.20.0
```

---

### 1.Homebrew를 통한 Node, Watchman 설치

```bash
$ brew install node
$ brew install watchman
```
---

### 2.새 프로젝트 생성 

```zsh
$ npx react-native init SampleProject
```
---

### 3.빌드 (Android)

```zsh
$ npx react-native run-android
```

![image-center](/assets/images/react_android_1.png){: .align-center}
---

### 4.빌드 (IOS)

```zsh
$ npx react-native run-ios
```
![image-center](/assets/images/react_ios_1.png){: .align-center}

<br>


참고 : [개발환경세팅](https://reactnative.dev/docs/environment-setup)
