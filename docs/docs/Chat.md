# Chat 명세

## 용어정리
유저 
채팅:
- 채널
	- 채널 소유자: 채널을 만든 유저
	- 채널 관리자: 채널의 관리 유저.
	- 채널 이용자: 일반유저
- DM

관리자 권한
- 추방, 차단, 음소거 (소유자에게는 불가능)

소유자 권한
- 채널 비밀번호 설정, 변경, 삭제
- 채널 이름 변경(optional)

---

## 해야 하는 일
- 유저를 위한 채팅을 만들어야 합니다.
- 유저는 공개 또는 비공개가 가능하거나 비밀번호로 보호될 수 있는 채널(채팅방)을 생성할 수 있어야 합니다.
- 유저는 다른 유저에게 직접 메시지(DM)를 보낼 수 있어야 합니다.
- 해당 유저는 다른 유저를 차단할 수 있어야 합니다. 이렇게 하면 차단한 계정에서 보낸 메시지가 더 이상 표시되지 않습니다.
- 새 채널을 생성한 유저는 채널을 떠날 때까지 자동으로 채널 소유자로 설정됩니다.
- 채널 소유자는 채널 접속에 필요한 비밀번호를 설정하고, 변경하고, 삭제할 수 있습니다.
- 채널 소유자는 채널 관리자입니다. 그들은 다른 유저를 관리자로 설정할 수 있습니다.
- 채널 관리자인 유저는 다른 유저를 추방하거나 차단하거나 음소거(제한된 시간 동안)할 수 있지만 채널 소유자에게는 할 수 없습니다.
- 유저는 채팅 인터페이스를 통해 다른 유저를 Pong 게임에 초대할 수 있어야 합니다.
- 유저는 채팅 인터페이스를 통해 다른 플레이어 프로필에 액세스할 수 있어야 합니다.

---


## 채널 object 구성
```json
채널 객체 데이터 {
	채널이름,
	(자동) 채널 Id,
	최대 인원,
	채널 소유자,
	채널 관리자 리스트(default 소유자),
	차단 리스트,
	is 비밀번호,
	채널 비밀번호,
	유저 리스트(음소거 옵션)
}
```


--- 

## event 명세

### 보내는 이벤트 (server)
##### 모두 가능
- 채널 만들기
	- 채널 목록에 등록
	- 채널 목록에서 확인 가능
	- 비밀번호 있으면 자물쇠 아이콘 달아주면 될듯
- 채널에 참여
	- 채팅 리스트 클릭해서 접속 -> 비밀번호 입력, 차단리스트 확인 후 참여
- 채널에 초대
	- 일단 초대하자 (비밀번호 스킵)
- 채팅
- 채팅으로 게임초대
	- 채널 내의 유저만 가능
#####  관리자 가능
- 강퇴
- 음소거
- 차단
- 관리자 지정
	- 유저 리스트 중 하나를 선택해서 관리자 리스트에 추가
##### 소유자 가능
- 패스워드 CUD
- 방제 바꾸기 ( 명세에는 없음 )

### 받는 이벤트 (client)
1. 채팅 받기
2. 게임 초대받기
4. 초대 당하기 -> 아무나 가능
3. 채널에서 강퇴 당하기

### DM
- 소유자, 관리자 없음
- 비밀번호 등등 설정 없음
- 유저 두 명만 존재
- 채팅
- 채팅으로 게임초대
	- 채널 내의 유저만 가능

---
### 논점
1. 밴을 어떻게 할 것인지
	1. 유저의 밴이 게임 매칭에 영향을 미치는지? -> 채팅은 채팅만 밴 가능.
		1. 근거: 블랙리스트로 잘하는 사람의 매칭을 피하는 악용 가능
	2. 밴은 해당 유저의 모든 채팅이 안보이게 설정
2. 채널 소유자가 방을 나가면 방폭!
3. 방을 만들때 비밀번호 세팅은 옵션으로 하자!
4. 채널 소유자와 채널 관리자 권한 관리를 어떻게 할지?
	1. 분리하고 채널 object 에서 관리
5. 채팅 인터페이스를 어떻게 구성할지
	1. 다른 유저 프로필에 접근 가능해야 함
	2. 게임에 초대 가능해야 함
6. DB 에 저장할지 메모리에 저장할지
	1. 일단 메모리에 저장하고 추후 DB 백업 논의


