# IRC 
IRC - Internet Relay chat
IRC란 internet Relay chat의 약자로 소켓 통신을 활용한 실시간 채팅 프로토콜이다.
해당 프로그램은 IRC SERVER를 구현하였다.

## 소켓 통신
소켓 : 

## 실행 방법
make 명령어로 MAKEFILE 실행 후 
./ircserv 8080(port) 1234(비밀번호) 실행
1. nc 명령어를 사용하는 방법
  nc -c $(서버 IP) $(port)
  ex) nc -c 127.0.0.1 8080
2. irssi 상용 클라이언트 사용
   brew install irssi\n
   ./irssi\n
   connect -nocap $(ip) $(port) $(password)\n
   ex) connect -nocap localhost 8080 1234
   irssi 클라이언트의 경우 명령어 작성 문법이 조금 상이 하므로 유의해주세요!
접속 완료 되었다면 
PASS, USER, NICK 명령어를 통해 회원 등록(irssi 클라이언트라면 생략가능)
기본적으로 명령어는 $(명령어) $(msg) 의 구조로 실행된다.
예를 들어 PASS 명령어의 경우 PASS 1234, NICK 명령어의 경우 NICK jonhan
JOIN 명령어의 경우 JOIN #test 이런식으로 작성하면 된다. 
   
