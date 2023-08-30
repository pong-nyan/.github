# Game 명세

## Start

<details>
<summary> Happy Case </summary>
<div markdown="1">
1. 본 게임은 1대1 랜덤 매칭게임이므로 대기열 큐로 관리
2. Options를 선택 후, Start 버튼을 누름

```
< Options >
 ㄴ Map : 무슨 맵?
 ㄴ 핀볼(main options) : 할 것인지?
 ㄴ 시간 갈 수록 공이 빨라짐 : 할 것인지?
 ㄴ 포탈(벽, 맵 중앙) : 할 것인지?
 ㄴ 중력(블랙홀, 화이트홀) : 할 것인지?
```

3. 플레이어를 큐에 삽입
4. 큐에 두 명이상 되었을 때, 선입선출방식으로 큐 앞단의 두 플레이어를 제거
5. 'game-'이라는 prefix + 두 플레이어의 소켓 join된 문자열 + '-(mode)' subfix를 통해 룸 생성
6. Player1과 Player2를 부여하고 Run 컴포넌트로 이동

</div>
</details>

<details>
<summary> Edge Case </summary>
<div markdown="1">

- 큐에 홀수명이 들어온 상태에서 플레이어의 소켓이 끊긴 경우

</div>
</details>


## Run
### 게임 구성요소

1. Any한 방식를 통해서 Options확인(ex. subfix)
2. 게임 카운트다운(3초)
3. 공 시작은 랜덤으로
4. 센서에 닿으면 페이지 전환
5. 페이지 구성
```
< 게임 페이지 기본 구성 >
 ㄴ 맵
 ㄴ Player1 / Player2
 ㄴ 공
```
```
< Score 페이지 기본 구성 >
 ㄴ 유저아이디, 점수
 ㄴ Player1   Player2
       ?    :    ?
```


### 시나리오
<details>
<summary> Happy Case </summary>
<div markdown="1">

1. 카운트다운 후 게임시작
2. 공이 랜덤 방향으로 출발
3. 센서에 닿으면 카운트 증가
4. 스코어 페이지 전환
5. 1 ~ 4 조건 충족까지 반복
6. 끝난 후 Total 페이지 전환

</div>
</details>

<details>
<summary> Edge Case </summary>
<div markdown="1">

- 공이 사라졌을 때
- Paddle이 맵 밖으로 나갔을 때
- Paddle 밀림 현상으로 인한 문제
- User가 게임 도중 나갔을 때

</div>
</details>

## End

```
< Total 페이지 기본 구성 >
 ㄴ Score 페이지 구성 가져오기
 ㄴ 승리자, 패배자 추가
 ㄴ Rank 점수 변동 추가(like 슈마메)
 ㄴ 'Main' or 'Restart' Button
```


### 시나리오
1. Button을 눌러서 게임 재시작 또는 게임 종료


### 추가 사항
- 사용자가 의도대로 start를 취소하고 싶은 경우 
- Rank Mode와 Normal Mode 구분
```
Rank Mode : Options이 랜덤하게 적용
Normal Mode : Options을 선택
```
- Game 방도 disconnect되었을 때 재접속 전략

