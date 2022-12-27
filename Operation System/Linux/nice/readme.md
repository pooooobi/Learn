# nice(프로세스 우선 순위)

1. nice란?
    - 리눅스 상에서 프로세스는 실행될 때 nice 라는 값을 갖고 실행된다.
    - nice 값은 프로세스간 실행 우선순위를 의미한다.
        - 예를 들어, 크고 리소스를 많이 차지하는 프로세스가 동작할 때, 우선순위가 높다면 아무런 동작을 할 수 없다.
        - 따라서, 무거운 프로세스에게 낮은 우선순위를 주어 다른 프로세스보다 덜 실행되게 만들어 효율적인 멀티태스킹 환경을 구성할 수 있다.

2. nice 값 정보
    - -20부터 19까지 줄 수 있다. (미지정시 default: 0)
    - nice 값이 낮을수록(-20에 가까울 수록) 우선순위가 높아진다.
    - nice 값이 높을수록(19에 가까울 수록) 우선순위가 낮아진다.
    - 일반 유저는 프로세스의 nice 값을 높여 우선순위를 낮추는 방향으로만 조절 가능한데, 우선 순위가 높은 특수한 프로세스를 지키기 위해서다.
        - 안되는건 아니다. `root`로 가능하다.
    - `ps -el`, `top`, `mpstat`의 명령어로 nice 값을 확인할 수 있다.

3. nice/renice 명령어
    - nice는 nice 명령어 실행 전 프로세스에 nice 값을 조정하여 프로세스를 실행시킨다.
    - renice는 이미 실행중인 프로세스의 nice 값을 조정한다.
    - `nice -n [n] [process]`: n만큼 프로세스의 nice 값이 증가한 상태로 프로세스 실행
        - `nice -[n] [process]`도 가능함.
    - `renice [n] [PID]`: 이미 실행중인 프로세스가 갖는 nice 값을 n으로 변경함

4. PRI?
    - 프로세스의 우선 순위를 논할 때, 나이스 값(NI) 이외에도 priority(PRI)가 존재한다.
    - 운영체제에서 참고하는 우선순위로 기억하면 된다.
        - 시스템 상황에 따라 부여되어 사용자 입장에서 조작할 수 없다.
    - `ps -l` 사용시 아래와 같은 화면이 나온다.
    ![ps -l 사용 화면](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6q0PD%2Fbtq90mHLVwD%2FLL9pL9VhJhafRWeUfCaXZ1%2Fimg.png)

5. 참고

    [출처](https://eyeballs.tistory.com/484)