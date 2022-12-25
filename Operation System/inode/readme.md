# 아이노드(inode)

1. inode에 대해
    - 운영체제에서 사용하는 파일 시스템중 하나다.
    - 기본 구조는 파일 시스템을 대표하는 수퍼 블록, 해당 파일 상세 정보, 일종의 PCB인 아이노드 블록, 실제 데이터를 담은 데이터 블록이 있다.
    - 파일 시스템에서 블록은 하나의 단위다. 대략 1~4KB 정도고, 하나의 파일엔 다수의 데이터 블록이 존재한다.

2. inode와 파일의 관계
    ![file block](https://velog.velcdn.com/images%2Fredgem92%2Fpost%2F7e7a2d3a-8cff-4c48-bfe6-76b16f099347%2Fimage.png)
    
    - 파일은 inode 고유 값과 자료구조에 의해 주요 정보를 관리한다.
    - 실제 사용자는 파일 이름으로만 인식하지만, 실제 컴퓨퍼는 `fileName:inode`로 파일과 inode 번호를 매칭시켜 인식한다.
    - 파일처리 방식
        1. 파일이 생성되자마자 inode 번호가 부여된다.
        2. inode 블록이 생성되어 상세정보 Meta-data가 기입된다.
        3. 이를 기반으로 파일에 접근한다.

3. inode 구조
    ![ext file system inode structure](https://velog.velcdn.com/images%2Fredgem92%2Fpost%2Fb832b64d-d3d9-4ceb-b08f-dcf286a4c0db%2Fimage.png)

    - inode 메타 데이터에는 권한, 소유주, 파일 크기, 생성 시간등의 정보를 담고 있다.

4. inode 구조와 파일 데이터
    ![inode structure & file data(meta)](https://velog.velcdn.com/images%2Fredgem92%2Fpost%2Fd9bcaff6-2ffc-4404-a40e-a892f490b769%2Fimage.png)

    - 파일의 용량이 클수록 데이터 정보를 담는 `Direct Block`의 크기를 늘리는 것은 비효율적이다. 따라서, Single Indirect, Double Indirect, Triple Indirect로 처리한다.
    - 각 Indirect는 4KB의 블록이다. 이 블록에 데이터를 담아 처리하는 것이 아닌, 특정 블록에 접근할 수 있는 주소를 갖고있다.
    - Single Indirect는 4KB / 4Byte => 1024개의 데이터 주소를 담는다.
    - Double Indirect는 Single Indirect의 주소를 1024개 담고 있다.
    - Triple Indirect는 Double Indirect의 주소를 1024개 담고 있다.
    - 이러한 구조를 통해 파일은 비교적 적은 블록을 갖고있어도 대량의 데이터를 관리할 수 있게 된다.

5. 참고

    [출처](https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EC%8B%9C%EC%8A%A4%ED%85%9C-inode-%EB%B0%A9%EC%8B%9D%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)