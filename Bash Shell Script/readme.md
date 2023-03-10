# Bash Shell Script

1. 유용한 Bash 커맨드 라인 단축키
    - `Tab` : 명령 자동완성
    - `Ctrl + c` : Interrapt Signal을 보내 실행중인 프로세스를 중단시킴
    - `Ctrl + a` : 라인 맨 앞으로 커서 이동
    - `Ctrl + e` : 라인 맨 뒤로 커서 이동
    - `Ctrl + r` : History 검색

2. 기초 명령어
- 파일 시스템
    - cd : Change Directory
        - cd - : 이전 디렉토리로 이동함.
    - ls : LiSt
        - `ls -arlth`를 기본으로 사용하는게 맘 편하다.
    - df : Disk Free
        - df -h를 주로 사용한다.
        - [Inodes](/Operation%20System/inode/readme.md)를 확인하려면 -i 옵션을 사용

- 디렉토리와 파일 통계
    - mkdir : MaKe DIRectory
    - rmdir : ReMove DIRectory
    - pwd : Print Working Directory
    - mount/umount
        - 디스크 장치를 표시하거나 가상 파일 시스템으로 지정한 디렉토리를 연결함
        - 가상 파일 시스템으로 지정할 때 주로 사용한다.
            - mount -t [FileSystemType] [IP Address]:[ROUTE] [Local Directory]
            - ex) mount -t nfs IP:/nfs /mnt -> IP주소의 nfs 폴더를 mnt 폴더로 마운트함
            - 접속을 끊을때는 `umount [경로]` 사용
    - stat
        - 지정한 파일의 파일 통계 출력
        - stat [FILE_NAME] 으로 사용한다.

- 파일 관련 명령어
    - touch
        - 지정한 이름의 비어있는 파일을 생성하거나 파일이 있는 경우 타임스탬프를 업데이트 한다.
    - cat : catenate
        - 지정한 파일의 내용을 출력한다.
    - head/tail
        - 지정한 파일의 1라인부터 지정한 라인까지 출력(default: 10)한다. -> head
        - 지정한 파일의 마지막 라인부터 지정한 라인까지 출력(default: 10)한다. -> tail
    - cp : CoPy
        - 지정한 파일을 지정한 위치와 이름으로 복사한다.
        - `cp -rfp [Original File Path]/[Name] [Copyed File Path]/[Name]`으로 사용하는 것이 편함.
    - mv : MoVe
        - 지정한 파일을 지정한 위치와 이름으로 이동한다.
    - rename
        - 지정한 규칙에 따라 여러 개의 파일 이름을 변경한다.
    - rm : ReMove
        - `rm -rf`로 사용하는 것이 편함.
    - less
        - 상하로 커서 이동이 가능한 파일보기
        - `cat` 보다는 긴 파일을 보기 유용하다.
    - ln : LiNk
        - 지정 파일에 대한 하드 링크 혹은 심볼릭 링크를 생성한다.
        - 옵션이 없으면 `하드 링크`를 생성하고, s 옵션을 추가하면 `심볼릭 링크`(윈도우의 바로가기)를 생성한다.
        - `s` 옵션을 추가한 `ln -s`를 주로 사용한다.
    - paste
        - 지정한 파일들의 행을 읽어 탭으로 구분하여 병합한다.
    - dd : Dataset Definition
        - 블록 단위로 데이터셋을 정의하며 파일을 쓰고 읽는다.
        - 실무에서는 랜덤 파일 생성, 디스크 성능 측정 용도로 자주 사용한다.
        - `dd if={input file name} of={output file name} bs={Byte(크기)} count={블럭을 복사할 횟수}`의 형식으로 사용한다.
            - bs를 구성하면 ibs, obs의 값도 자동으로 정해주기 때문에 별도로 지정하진 않아도 된다.
    - tar : Type ARchive
        - 지정한 데이터 및 디렉토리를 하나의 파일로 만든다 -> 압축한다.
        - 파일을 묶을 때에는 `tar -cvzf 타르볼 파일명 디렉토리/파일명`
        - 파일을 풀때에는 `tar -xvzf 타르볼 파일명`
        - `.tgz` 파일 확인시에는 `tar -tf 파일명`

- 프로세스 관련 명령어
    - ps : Process Status
        - 시스템에서 실행중인 프로세스에 대한 정보를 출력한다.
        - `ps -ef`는 UID, PID, PPID 등의 정보를 출력한다.
        - `ps aux`는 위의 정보를 포함하여 CPU, MEMORY(가상 포함) 등의 정보도 출력된다.
        - CMD의 줄이 잘려있는데 더 길게 보고싶다면 `ps axfwwwww` 로 확인. w의 개수에 따라 명령어의 출력 라인수가 늘어남. 요즘 엔지니어는 잘 쓰지 않는 방법... (트리도 나옴)
    - pstree : Process Status TREE
        - 시스템에서 실행중인 프로세스에 대한 정보를 트리 구조로 출력한다.
    - top
        - 프로세스 목록을 일정 시간마다 새로고침하여 화면에 출력하는 툴
        - 시스템 전반적인 상황을 알 수 있다.
        - 맥에서는 사용법이 다르다.
            - o를 누르면 갱신 주기마다 높은 값 지정할 수 있다.
        - CPU
            - us : 유저가 사용한 시간
            - sy : 시스템이 사용한 시간
            - ni : [nice](/Operation%20System/Linux/nice/readme.md) 값에 따라 우선순위가 변경된 프로세스가 실행한 시간
            - id : Idle time, 유휴 시간
            - wa : Wait, I/O 장치를 기다리는데 소요된 시간
            - hi : Hardware Interrupt
            - si : Software Interrupt
            - st : Still time, 가상화된 프로세스를 처리하는데 비 자발적으로 기다린 시간
    - nohup : NO HangUPs
        - 쉘 스크립트 파일을 데몬 형태로 실행한다.
        - 표준 출력을 지정한 파일로 리다이렉트
        - 프로그램이 종료되기 전까지 백그라운드로 실행하는 명령어다.
    - kill
        - 지정한 프로세스에 지정한 시그널(SIG)을 보내 프로세스를 종료시킨다.
        - Sofrware Interrupt에 속한다.
        - 좀비 프로세스를 종료할 수 있는 유일한 방법이다.
        - `INT(2)`, `TERM(15)`, `KILL(9)` 정도의 종료 시그널을 알면 좋다.
            - `KILL -SIG(혹은 번호) PID`로 사용한다.
            - ex) KILL -INT PID

- 네트워크 관련 명령어
    - 참고
        - RedHat : `/etc/sysconfig/network-scripts` 에서 `ifcfg` 파일
        - Ubuntu : `/etc/network/interfaces`
    - ifconfig : InterFace CONFIGuration
        - 네트워크 인터페이스의 활성/비활성화 및 설정
        - eth0의 정보를 조회하고 싶다면? `ifconfig eth0`
    - ip
        - IP 관련 정보조회 및 설정
        - eth0의 정보를 조회하고 싶다면? `ip address show eth0` 혹은 `ip ad sh eth0`
            - 위의 ifconfig 보다는 좀 긴 편이다.
    - netstat : NETwork STATistics
        - 네트워크 프로토콜의 통계와 연결 상태를 출력
        - `netstat -nltpu`, `netstat -tanu`를 주로 사용한다.
            - n : IP나 포트 번호를 숫자로 보여줌(http -> 80 등)
                - 알고싶다면 `/etc/services` 열어보면 된다.
            - l : LISTEN(특정 포트를 열고 유저의 접속을 기다림) 소켓을 보여줌
            - t : TCP
            - p : 프로그램의 이름 출력
            - u : UDP
    - ss : Socket Statistics
        - 네트워크 소켓의 통계와 연결 상태를 출력
        - 위와 마찬가지로 `ss -nltpu`, `ss -tanu`를 주로 사용한다.
    - iptablets
        - 패킷 필터링 도구
        - 패킷의 출입을 제한하는 방화벽 구성, NAT(Network Address Translation) 구성에 사용함
        - 목록을 확인하고 싶다면 `iptablets -nL`
            - 만약 목록이 안나온다면 방화벽이 꺼져있는지 `systemctl status iptablets`로 `Active`를 확인해보자.
                - 죽었으면 `systemctl start iptablets`로 실행하자.
            - L : List
        - Chain INPUT : 외부에서 서버로 들어오는 클라이언트에 대한 규칙
        - Chain Forward : 해당 서버를 경유하여 통과하는 클라이언트에 대한 규칙
        - Chain OUTPUT : 해당 서버에서 외부로 나가는 통신에 대한 규칙
    - ufw : Uncomplicated FireWall
        - iptables의 제어를 쉽게 하기 위한 도구
    - ping
        - ICMP 프로토콜의 응답 확인 도구
    - wget : World wide web + GET
        - 웹 서버로부터 컨텐츠를 가져오는 도구
    - curl : Client for URLs
        - 다양한 프로토콜을 사용하여 데이터를 전송하게 해주는 도구
        - `curl -Lkso /dev/null -w  "%{http_code}%" 주소` 즉, HTTP STATUS CODE를 받기 위해 주로 사용함(서버를 다루는 입장에서).
            - L : Redirect(301)의 경로를 따라가게 함
            - k : HTTPS 인증 무시 옵션
            - s : Silent mode로 실행. 통계값을 출력하지 않음.
            - o : Output file, /dev/null로 지정하면 아무것도 출력되지 않음.
            - w : Output Format을 결정함.
    - route
        - 네트워크의 경로 정보(라우팅 테이블) 출력 및 변경해주는 도구
        - 정보 조회(`route`, `route -n` -> 이름 대신 숫자 출력)
            - Destination : 경로
            - Gateway : 게이트웨이
            - Genmask : 목적지 네트워크의 netmask 주소
            - Flags : 해당 경로의 대한 정보를 알려주는 기호
                - U : UP, 이 경로가 살아있음
                - H : HOST, 호스트를 의미
                - G : Gateway, 게이트웨이로 향하는 경로
            - Metric : 네트워크 목적지 까지의 거리
            - Ref : Reference, 경로를 참조한 횟수
            - Use : 경로를 탐색한 횟수
            - Iface : Interface, 어떤 인터페이스를 사용했는지
        - 추가 및 삭제
            - `route add`, `route del`로 사용.
            - 주로 추가 및 삭제보단 확인하는 용도로 사용할 확률이 높음.

- 검색 및 탐색 관련 명령어
    - find
        - 지정한 파일명이나 정규 표현식을 이용하여 파일을 검색
        - `find [option] [find start path] [expression]`의 구조로 사용한다.
            - expression -> 파일의 이름, 퍼미션, 업데이트 날짜, 파일 생성 날짜 등을 지정하여 찾을 수 있게 함.
                - 표현식에 들어갈 수 있는 것들은 name, type(파일 f, 디렉토리 d), perm(permission), empty 등이 있다.
            - 예시로, 어딘가에 존재한 파일을 찾고싶다면 `find ./ -name [file name]`의 구조로 찾으면 된다.
                - 결과값으로 해당 파일이 존재한 path가 출력된다.
    - which
        - 환경변수 PATH에 등록된 디렉토리에 있는 명령어를 찾아주는 도구
            - 환경변수를 확인하고 싶다면 `echo ${PATH}`
        - 명령어를 찾아주는 도구이며, 쉘 스크립트 사용시 명령어 전체 위치를 적어주어야 하는 경우가 있어 사용한다.
        - ex) which ls
    - grep : Global / Regular Expression / Print
        - 참고(로그 위치)
            - RedHat : /var/log/messages
            - Ubuntu : /var/log/syslog
        - 텍스트 검색 기능을 가진 도구
        - 파일이나 표준 입력을 검색하여 지정한 정규 표현식과 맞는 줄을 출력
        - `grep -[option] "[찾을 문자열]" 파일명`으로 사용하며, 주로 `grep -ir "찾을 문자열" 파일명`을 많이 사용한다.
            - ex) grep "error" /var/log/* 등
            - i 옵션을 넣으면 찾을 문자열에 대해 대소문자 구분을 하지 않는다.
            - r 옵션을 넣으면 하위 디렉토리도 찾아준다.
    - history
        - 명령어를 수행한 목록을 출력 및 조작
        - `/.bash_history`에 저장되어 있다.

- I/O 관련 명령어
    - redirection
        - 표준 스트림(stdin, stdout, stderr)을 부등호를 이용하여 지정한 위치로 보낼 수 있는 방향지정 옵션
        - `명령 리다이렉션기호 파일명`으로 사용한다.
        - `>`, `>>`, `>|`의 옵션이 있다.
            - `>` : 매번 초기화
            - `>>` : 기존 내용에 추가
            - `>|` : 없는 파일을 생성시킴
    - echo
        - 문자열을 출력하는 도구

- 유저 관련 명령어
    - chmod : CHange MODe
        - 파일이나 디렉토리의 접근권한을 변경하는 도구
        - 권한은 rwx(READ, WRITE, EXECUTE)로 구성되어 있다.
        - 순서대로 소유주, 그룹, 외부 사용자 순으로 구성되어 있다.
            - ex) rwxrwx---(외부 사용자를 제외하고 모두 권한이 있음)
    - chown : CHange the OWNer of a file
        - 파일의 소유권을 바꾸기 위한 도구
    - sudo : SUperuser DO --> Substitude User Do
        - root 사용자의 보안 권한을 이용하여 명령 또는 프로그램을 실행하는 도구
    - who
        - 현재 시스템에 로그인한 사용자 목록을 출력

- 기타 명령어
    - date
        - 날짜를 표시해준다.
        - `d` 옵션을 자주 사용하고, 1일 전 날짜를 알고싶다면 `date -d '1 day ago'`와 같이 사용하면 된다. 미래는 `ago`만 빼면 된다.
        - `week/month/hour/minute/second`의 키워드를 붙여 사용하자.
        - 만약 출력 방식을 년-월-일 시:분:초 로 변경하고 싶다면 `date '+%Y-%m-%d %H:%M:%S'`와 같이 사용하면 된다. 응용해서 다른것도 사용하자.
    - seq : SEQuence
        - 지정한 규칙으로 숫자열을 출력하는 도구
        - `seq 시작숫자 끝숫자`의 형식으로 사용한다.
        - 옵션
            - w : 끝 숫자에 맞는 자릿수에 따라 0이 추가됨(1~10까지면 01, 02, ..., 10)
            - f : 지정한 형식대로 나옴
                - `seq -f %0자릿수g`의 형식이다.
    - more
        - 한 화면씩 지정한 파일의 내용을 출력하는 도구
        - CLI 출력에서 유용하게 사용된다.
    - watch
        - 지정한 명령어를 지정한 시간(초)마다 재실행하여 화면에 출력하는 도구
        - 옵션 `-n 초`를 통해 시간 지정이 가능하다.
    - crontab
        - 리눅스의 잡 스케쥴러의 내용을 출력하거나 편집할 수 있는 도구
        - 출력은 `-l` 옵션을 추가하고, 편집은 `-e` 옵션을 추가한다.
        - crontab에 등록된 모든 스케쥴을 제거할때는 `-r` 옵션을 사용하면 되는데, 자주 쓰지도 않고 중요하지도 않으니 사용 전 주의하자.

3. 쉘 스크립트 기본
- 명령어 연속 실행
    - `파이프라인(|)` : 파이프라인 왼쪽 명령결과 표준 스트림을 오른쪽 명령의 입력으로 사용
    - `세미콜론(;)` : 세미콜론 왼쪽의 명령이 끝난 후 이어서 오른쪽의 명령을 실행함
    - `AND 조건(&&)`
        - AND의 연산이 하나라도 false일 경우 모든 결과가 false인 특징을 이용
        - AND 좌측 명령/테스트의 결과가 true이면 우측의 명령을 실행
        - AND 좌측 명령/테스트의 결과가 false이면 우측 명령을 실행하지 않음(이미 거짓이며, AND의 연산이 false 이므로)
    - `OR 조건(||)`
        - OR 연산의 하나라도 true일 경우 모든 결과가 true인 특징을 이용
        - OR 좌측 명령/테스트의 결과가 true이면 우측 명령을 실행하지 않음(이미 참이며, OR 연산이 true 이므로)
        - OR 좌측 명령/테스트의 결과가 false이면 우측 명령을 실행
    - 참고 : [단락 평가(Short-circult Evaluation)](https://github.com/pooooobi/Swift/tree/main/Swift%20Theory/Operators/Advanced%20Operators), 리눅스도 같은 방식임.

4. CLI(Command Line Interface)
- nano
    - 리눅스 터미널 환경에서 직관적인 사용자 인터페이스를 제공하는 편집 도구
    - 학습 난이도가 매우 낮음
- vim : Vi Improved
    - 리눅스 터미널 환경에서 사용자 인터페이스를 제공하는 편집 도구
    - vi의 업그레이드 버전이며, 최근에는 neovim이라는 이름으로 vim의 refector 버전이 나옴.

5. 간단한 쉘 스크립트
- 조건문
    - 조건에 따라 명령어를 실행하거나 실행하게 하지 않는다.
    ```bash
    if [조건문 1]; then # 조건문 1이 참일경우 실행할 명령어
    elif [조건문 2]; then # 조건문 1이 거짓이고, 조건문 2가 참일경우 실행할 명령어
    else # 조건문 1, 2가 거짓일 경우 실행할 명령어
    fi
    ```
    - 조건문이 여러개가 필요하다면 `-a`, `-o` 붙여서 사용하면 된다.

- 비교문
    |비교문|설명|비고|
    |:---:|:---:|:---:|
    |A -eq B|A와 B가 같은가|숫자|
    |A -ne B|A와 B가 같지 않은가|숫자|
    |A -ge B|A가 B보다 크거나 같은가|숫자|
    |A -gt B|A가 B보다 큰가|숫자|
    |A -le B|A가 B보다 작거나 같은가|숫자|
    |A -lt B|A가 B보다 작은가|숫자|
    |A = B|문자 A, B가 같은가|문자열|
    |A != B|문자 A, B가 다른가|문자열|
    |A < B|문자열 A가 B보다 작은가(바이트)|문자열|
    |A > B|문자열 B가 A보다 작은가(바이트)|문자열|
    |-n A|A의 문자열 길이가 0보다 큰가|문자열|
    |-z A|A의 문자열 길이가 0인가|문자열|
    |-d file|파일이 존재하고 디렉토리인가|파일|
    |-e file|파일이 존재하는가|파일|
    |-f file|파일이 존재하고 파일인가|파일|
    |-r file|파일이 존재하고 읽을 수 있는가|파일|
    |-s file|파일이 존재하고 비어있지 않은가|파일|
    |-w file|파일이 존재하고 쓰기가 가능한가|파일|

- case 문법
    - 조건이 많을 경우 if보다 가독성 있게 작성할 수 있다.
    ```bash
    case 변수 in
    패턴 1)
        # 패턴 1이 참일경우 실행할 명령어
    패턴 2)
        # 패턴 2가 참일경우 실행할 명령어
    *)
        # 위에서 지정한 모든 패턴에 해당되지 않는 경우 실행
    esac
    ```

- for/while
    ```bash
    for 변수 in 변수에 넣을 데이터
    do
        데이터가 끝날 때까지 반복해서 실행할 명령어
    done

    while 조건문
    do
        조건이 참인 동안 반복해서 실행할 명령어
    done
    ```

- function
    ```bash
    function 함수명 {
        명령어
    }
    ```

- 배열
    - 배열에 숫자 또는 문자 사용 가능

- 리다이렉션
    - 입력/출력/에러(표준 스트림)를 지정한 곳으로 바꿔준다.
    - 쉘 스크립트 안에서 텍스트 파일의 활용