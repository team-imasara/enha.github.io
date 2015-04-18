  * 상위 항목 : [컴퓨터 관련 정보](%EC%BB%B4%ED%93%A8%ED%84%B0%20%EA%B4%80%EB%A0%A8%20%EC%A0%95%EB%B3%B4.md)  

**New Technology File System**

## Contents

    

1. 개요 
2. FAT와의 차이점 

[[edit](http://rigvedawiki.net/r1/wiki.php/NTFS?action=edit&section=1)]

## 1. 개요 ¶

  

[마이크로소프트](%EB%A7%88%EC%9D%B4%ED%81%AC%EB%A1%9C%EC%86%8C%ED%94%84%ED%8A%B8.md) OS인 [윈도우즈](%EC%9C%88%EB%8F%84%EC%9A%B0%EC%A6%88.md)의
[파일](%ED%8C%8C%EC%9D%BC.md) 시스템이다. MS-DOS와 이전 버전의 윈도에서 쓰였던 마이크로소프트의 이전 FAT
파일 시스템을 개선하여 만든 새로운 파일 시스템이다. [FAT](FAT.md)시스템에 비해 몇 가지 개선사항이 있는데, 메타데이터의
지원, 고급 데이터 구조의 사용으로 인한 성능 개선, 신뢰성, 추가 확장 기능을 더한 디스크 공간 활용을 들 수 있다.

  

처음 나올 당시엔 매우 획기적인 파일시스템이었으나, 21세기 들어 오픈소스 진영이 폭발적으로 발달하면서 NTFS 에 비교해도 전혀 떨어지지
않는 다양한 파일시스템들이 선보이게 되었고, 그 파일시스템계를 평정한 SUN 의 ZFS 까지 등장하면서 현재는 그냥 그럭저럭인 파일시스템이
돼버렸다. MS는 뒤쳐지지 않기 위해 NTFS를 기반으로하는 ReFS를 준비중이다. [MSDN의 ReFS
설명](http://blogs.msdn.com/b/b8_ko/archive/2012/01/21/windows-refs.aspx)

  

최초로 발표된 건 Windows NT 3.1 이 발매된 1993년. 즉, Windows NT와 함께 탄생하였다. 현재 주로 쓰이는 NTFS
인 3.1 은 윈도 XP 부터 사용되었으며, 이는 하위호환으로 Windows NT 3.51 의 1.2 버전부터 사용할 수 있다. (3.50
이전과는 호환 안됨)

  

이 밖에도 파일 암호화라든지 수많은 기능을 가지고 있지만 역시 유저들에게 와닿는 기능은 파일용량 한계의 완화일 것이다. 특히 DVD 의
보급으로 4 GB가 넘는 ISO 파일을 FAT32 에선 저장하질 못해`[1]` Windows 2000 이 빠르게 소비자 시장에 퍼지게 된
원인이기도 하다. (Windows NT 3.51 은 Windows 9x 계열과 드라이버 호환성이 상당히 떨어졌기 때문에) 특히, 윈도 XP
부터는 아예 하드나 이동식 디스크의 용량이 32GB 가 넘으면 무조건 NTFS 로 포맷하도록 해버렸기 때문에, 구형시스템에서 USB
외장하드를 쓰기 위해 FAT32 로 포맷하려면 서드파티 포맷 툴을 써야만 했다.

  

NTFS 에도 약간의 제한이 있는데, 가장 큰 제한은 파일명 포함 최대 260 자로 제한된 경로명. 사실, 이것은 NTFS 자체의 제한은
아니다. 원래 윈도의 NT커널은 32,767 자까지 지원할 수 있다. 다만, Win32 API 의 MAX_PATH 가 260 자로 제한된것이
문제. 아직도 Win32 API 를 이용한 프로그램들이 상당히 많고, 더 웃픈것은, MS
Explorer([탐색기](Windows%20%ED%83%90%EC%83%89%EA%B8%B0.md))에서 기본적인 복사 명령도
WIN32 API 를 사용하여 저런 제한에 딱 걸린다는것이다. (...)`[2]`

  

덕분에 MS Explorer 네트워크상에서 저런 제한이 없는 다른 OS 다른 파일시스템에서 NTFS 로 자료를 카피할때 파일경로
길이제한때문에 카피 못한다는 메시지가 뜨는경우가 있고, 이것을 NTFS 파일시스템의 한계로 알고있는 사람도 적지않다. 다른 카피프로그램을
사용하거나 기타등등 우회방법이 있긴 한데, 많이 귀찮아서 좀 불편해도 그냥 260 자 안으로 파일경로를 구성하는 사람들이 많다.`[3]`

  

또한, NTFS 는 원래 2의 64승으로 거의 무한대에 가까운 파티션 제한용량을 가지고 있지만 Windows XP 부터 지금까진 2의
32승인 256 TB 까지만 저장 가능하다. 거기다 논리 파티션 하나당은 16 TB 가 한계. MBR 레코드가 위치하는 부트파티션은 한계가
2TB 까지 내려간다. 이 제한은 64비트 운영체제로 가야만 풀린다. 즉, 2TB보다 용량이 큰 하드디스크는 32비트 운영체제에서는 하나의
파티션으로 쓸 수 없다! 하지만 파일 용량 제한은 32비트에서도 파티션 하나 꼭 채우는 16 TB 이므로 큰 문제는 아니다. 참고로,
NTFS 의 압축파티션 기능이 작동하려면 클러스터 용량은 반드시 4KB 이하가 되어야만 한다. 이보다 큰 클러스터는 압축기능을 지원하지
않는다.

  

NTFS 시스템에는 인덱싱 기능이 있는데 이를 적극적으로 활용하는 윈도 비스타 이후부터는 컴퓨터를 깔자마자 며칠간은 하드 데이터를
인덱싱하느라 컴퓨터가 좀 느릴 수도 있다. 하지만 일단 분석이 끝나면 XP 보다 쾌적하게 이용할 수 있다는 평이 많은 편.

  

[UEFI](UEFI.md) 부팅을 지원하지 못하기 때문에 USB로 부팅 디스크를 만드려면 exFAT로 포맷해야 하며, MS에서
제공하는 인스톨러가 아닌 서드파티 툴을 써야 한다.

  

[더블스페이스](%EB%8D%94%EB%B8%94%EC%8A%A4%ED%8E%98%EC%9D%B4%EC%8A%A4.md)(드라이브스페이
스)는 지원하지 않는다. 애초에 NTFS는 고유의 압축 기술이 있는데다가 Windows ME가 출시되기 전쯤부터 더블스페이스는 하드디스크의
대용량화로 이미 사양길을 걷고 있었다. 따라서 오늘날 더블스페이스는 사실상 사장된 유틸리티이므로 개의치 않아도 된다.

  

[[edit](http://rigvedawiki.net/r1/wiki.php/NTFS?action=edit&section=2)]

## 2. FAT와의 차이점 ¶

  * FAT와 NTFS 모두 파일 이름을 따로 기록하는 구간은 가지고 있다. 하지만 FAT는 표 형태로 저장하고 NTFS는 B+ tree로 저장한다.
  * NTFS에는 저널링 파일 시스템이 있는데, 이것은 파일 시스템의 오류를 줄여주고 디스크 검사 속도를 높여주는 것으로, 파일을 기록하기 전에는 '어디어디 데이터 기록 예정'이라는 데이터를, 그리고 파일 기록이 끝난 후 '데이터 기록 완료'라는 데이터를 기록하는 곳이다.

`\----`

  * `[1]` 하필이면 DVD의 용량이 4GB를 조금 넘어가는 4.3GB다.(싱글 레이어 기준)
  * `[2]` 최신 버전인 윈도우 8.1도 다를 바 없다.
  * `[3]` 과거 빌게이츠의 "메모리는 640kb 면 충분하다" 드립과 엮어서 "PATH 는 260 자면 충분하다" 는 드립도 가끔 나온다. 
