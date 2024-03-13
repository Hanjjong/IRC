# IRC 
IRC - Internet Relay chat</br>
IRC란 internet Relay chat의 약자로 소켓 통신을 활용한 실시간 채팅 프로토콜이다.</br>
해당 프로그램은 IRC SERVER를 구현하였다.</br>


# 소켓 통신

소켓(Socket)은 TCP/IP 기반 네트워크 통신에서 데이터 송수신의 마지막 접점을 말합니다. 소켓 통신은 이러한 소켓을 통해 서버-클라이언트 간 데이터를 주고받는 양방향 연결 지향성 통신을 말합니다. 보통 지속적으로 연결을 유지하면서 실시간으로 데이터를 주고받아야 하는 경우에 사용됩니다.

소켓은 클라이언트 소켓과 서버 소켓으로 구분되며, 소켓 간 통신을 위해서는 네트워크상에서 클라이언트와 서버에 해당되는 컴퓨터를 식별하기 위한 IP 주소와 해당 컴퓨터 내에서 현재 통신에 사용되는 응용 프로그램을 식별하기 위한 포트 번호가 사용됩니다.

## Kqueue()

kqueue는 커널에 할당된 폴링 공간(kernel event queue - kqueue)에 모니터링할 이벤트를 등록하고, 발생한 이벤트를 return 받아 Multiple I/O Event를 처리할 수 있도록 도와줍니다.

이벤트 등록 및 반환은 kevent 구조체를 통해 이루어지며, 구조체 필드로 존재하는 이벤트에 대한 필터, 플래그 등을 이용해 다양한 이벤트 발생 상황에 대한 정의 및 발생 이벤트에 대한 정보 확인을 할 수 있습니다.

`kqueue()`를 통해 커널에 새로운 event queue를 만듭니다. 그 event queue의 fd를 반환합니다. 이 fd를 통해 kqueue()에서 이벤트를 등록하고 관리할 수 있습니다. kqueue는 fork로 인한 자식 프로세스에 상속되지 않습니다.

```cpp
int kevent (
    int kq, // kqueue의 fd
    const struct kevent *changelist, // 등록하고자 하는 이벤트
    int nchanges, // changelist의 길이
    struct kevent *eventlist, // 발생한 이벤트들
    int nevents, // eventlist의 길이
    const struct timespec *timeout // timeout
);

```
- kevent()에서 중심이 되는 데이터가 struct kevent입니다.
```cpp
struct kevent {
    uintptr_t ident; // 이벤트에 대한 식별자, fd 번호
    int16_t filter; // 이벤트에 대한 식별자, 이벤트의 종류에 해당
    uint16_t flags; // event를 적용시키거나, event가 return 됐을 때 flag
    uint32_t fflags; // filter에 대한 flag
    intptr_t data; // filter에 대한 data
    void *udata; // user data
};
```
- flags
    
    어떤 액션을 취할 지 결정한다.
    
    EV_ADD: 이벤트를 kqueue에 추가한다.
    
    EV_ENABLE: kevent()가 해당 이벤트가 발동됐을 때, 반환할 수 있도록 한다
    
    EV_DISABLE: kevent()가 해당 이벤트를 무시하도록 한다.

## 실행 방법
make 명령어로 MAKEFILE 실행 후 </br>
./ircserv 8080(port) 1234(비밀번호) 실행</br>
1. nc 명령어를 사용하는 방법</br>
  nc -c $(서버 IP) $(port)</br>
  ex) nc -c 127.0.0.1 8080</br>
2. irssi 상용 클라이언트 사용</br>
   brew install irssi</br>
   ./irssi</br>
   connect -nocap $(ip) $(port) $(password) </br>
   ex) connect -nocap localhost 8080 1234</br>
   irssi 클라이언트의 경우 명령어 작성 문법이 조금 상이 하므로 유의해주세요!</br>
접속 완료 되었다면 </br>
PASS, USER, NICK 명령어를 통해 회원 등록(irssi 클라이언트라면 생략가능)</br>
기본적으로 명령어는 $(명령어) $(msg) 의 구조로 실행된다.</br>
예를 들어 PASS 명령어의 경우 PASS 1234, NICK 명령어의 경우 NICK jonhan</br>
JOIN 명령어의 경우 JOIN #test 이런식으로 작성하면 된다. </br>
   
