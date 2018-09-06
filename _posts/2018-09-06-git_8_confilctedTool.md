---
layout: post
title: "충돌 병합 Tool"
tags: [ git, sourcetree, diff  ]
date: 2018-09-06
categories: [ git ]
---

<p align="center">
    브랜치들을 병합할 때 일어나는 충돌은 프로젝트가 복잡해 질 수록 해결하기 어려워 질 수 있기 때문에 충돌사항을 좀 더 편하게 도와줄 수 있는 도구들이 있다.
</p><br/>

# diff 도구
<font color="deeppink">파일간의 차이 또는 같은 파일의 다른 버전간의 차이를 구분해 주는 도구를 'diff도구'</font>라고 한다.<br/>
소스 트리에서 볼 수 있는 빨간색 녹색 표시등도 이런 도구들을 이용한 것이다.<br/>

하지만, 소스트리의 기본 diff도구는 매우 기능이 적기 때문에 충돌 시 모든 작업을 수작업을 통해서
수정해야 한다. 따라서, 자동으로 좀 더 간편하게 처리할 도구가 필요할 경우 다른 diff도구를 사용하면 된다.
- 추천 : beyond compare (유료)

#### ▶ diff도구 적용방법
소스트리의 <font color="orange">'Tools-Options-Diff'</font> 탭으로 들어가보면 <font color="orange">'External Diff Tool'</font>을 선택할 수 있다.

#### ▶ diff도구 사용법
소스트리에서 파일 오른쪽 클릭 후 <font color="orange">External diff</font>를 클릭하면 왼쪽오른쪽 화면으로 나뉘는 수정전과 수정후의 차이점을 볼 수 있는 diff도구가 실행된다.<br/>

- 충돌 발생시<br/>
충돌이 발생한 '!'파일을 오른쪽 클릭 후 <font color="orange">Resolve Conflicts"-> Launch External Merge Tool</font>을 클릭하면 diff툴이 실행되고 '공통된 부모버전(BASE)' / '현재브랜치수정파일(LOCAL)' / '추가브랜치수정파일(REMOTE)'을 한번에 비교할 수 있다.<br/>

<br/>