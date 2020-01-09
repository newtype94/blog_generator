---
title: ubuntu
date: 2020-01-07 02:28:05
tags:
    - ubuntu
    - 방화벽
category: 
    - 서버관리
    - ubuntu
---

# 찾기
## find [경로] [옵션] [파일명]
" * = any string " 이라는 점을 활용
- find / -name '*.png'
  - 최상위 디렉토리, (root)에서 부터 검색을 해서 확장자가 png로 끝나는 모든 파일을 찾는다.
- find / -name 'afreeca*' 
  - afreeca로 시작하는 모든 파일을 찾는다.
- find / -name '1676075537'
  - 이름이 '1676075537'인 모든 파일을 찾는다.
- find -name 'fileName'
  - 경로를 생략하고 명령어를 입력하면 해당 디렉토리에서부터 그 하위 디렉토리까지 찾는다.

***

# 삭제
## rm [option] [folderName]
옵션은 아래 세가지를 이어붙여서 사용
1. r : 파일 디렉토리 함께 삭제하기
2. f : 파일 유무와 상관없이 삭제하기
3. v : 어떻게 완료되었는지 설명하기

***

# 방화벽
### 방화벽 룰 설정파일
    /etc/iptables/rules.v4
### 방화벽 룰 저장
    netfilter-persistent save
### 설정 완료 후 재시작
    netfilter-persistent reload
### 리눅스에서 현재 열려 있는 포트를 확인하는 방법
    열려 있는 모든 포트를 표시하기 : netstat -nap
- n:host명으로 표시 안함
- a:모든소켓 표시
- p:프로세스ID와 프로그램명 표시

### LISTEN중인 포트를 표시하기
	netstat -nap | grep LISTEN)

### 상대방 포트가 열려 있는지를 확인하는 방법 : netcat(nc)
	nc -z 호스트주소 포트
	- ex) nc -z www.google.com 80
- z: 포트 검색
	
### 상대의 포트 범위를 지정하여 열린 포트를 확인하기
	nc 호스트주소 -z 시작포트-끝포트
	ex) nc 10.20.30.40 -z 19-21

### 포트를 열기
#### 포트가 LISTEN중이다 + 상대방 호스트에서 포트가 열려있지 않다고 나온다 => 호스트의 포트가 막혀 있다.
    iptables -I INPUT 1 -p tcp --dport 3000 -j ACCEPT 
    외부에서 들어오는(INBOUND) TCP포트 12345의 연결을 받아들인다는 규칙을 방화벽 1번 방화벽 규칙으로 추가한다.
- I: 새로운 규칙을 추가한다.
- p: 패킷의 프로토콜을 명시한다.
- j: 규칙에 해당되는 패킷을 어떻게 처리할지를 정한다.
	
    
### 조회
	iptables -L -v
- L: 규칙을 출력
- v: 자세히

### 삭제
추가할 때 명령어의 "-I"를 "-D"로 바꾸어 준다
#### 규칙번호로 삭제하기
	iptables -D INPUT 1
    - D: 규칙을 삭제
#### 추가한 규칙으로 삭제하기
	iptables -D INPUT -p tcp --dport 12345 -j ACCEPT 