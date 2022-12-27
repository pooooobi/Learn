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
    