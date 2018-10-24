---
title: "XCode에서 ObjC 플래그"
categories:
  - OSX
tags:
  - OSX

last_modified_at: 2018-10-24T01:34:52-05:00
---

This flag causes the linker to load every object file in the library that defines an Objective-C class or category. While this option will typically result in a larger executable (due to additional object code loaded into the application), it will allow the successful creation of effective Objective-C static libraries that contain categories on existing classes.
(출처: https://stackoverflow.com/questions/6629979/what-does-the-objc-linker-flag-do)

이 플래그를 써주면 라이브러리 프로젝트에서 사용한 프레임워크를 일일이 업로드해줄 필요가 없다. 이를 안써주면 Objective-C의 카테고리를 사용할 수 없으며, 카테고리로 구현한 클래스들을 일반 클래스로 다시 변환해주어야한다. (Objective-C 같은 C 계열 언어에서 프리픽스의 중요성을 깨달은 일과 관련하여 메모..)
