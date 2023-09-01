# 요구사항

## Purpose
This project is about creating a website for the mighty Pong contest!

## Implements
- nice user interface
- chat
- real-time multiplayer online games
- Conditions
- NestJS
- Typescript framework
- latest stable version library
- PostgreSQL, no other database
- SPA (possible browser back, forward button)
- Chrome, other browser support
- must handle error
- docker-compose up --build, make all done.

### Security concerns
- password hashed
- SQL injections
- server-side validation

### User Account
- OAuth of 42 intranet
- Unique user name (처음 회원가입시 이미지와 닉네임 수정 가능)
- two-factor authentication (QR, email, google authenticator, ARS, 지민인식, 홍채인식, face checking)
- friends, see their status
- Stat in profile
- History, ladder -> public
- 
### Chat
public(공개방), private(초대로만 접속), protected(접속시 비번) by password channel
DM
    a. 여러가지 케이스 고려해야함. (TODO)
block
channel
    a. creator is automatically channel owner.
    b. owner can C_UD password
    c. administrator can kick, ban, mute(for a limited time) / (except for owner)
invite through chat a. e.g. /invite seongyle
access other players profiles through the chat interface

### Game
- You have to offer the best user experience possible
- users should be able to play a live Pong game versus another player directly on the website
- matchmaking system a. the user can join a queue until they get automatically matched with someone else
- customization options (e.g. app skin, skill)
- The game must be responsive!
