# Linux

---
# 리눅스 명령어
### DIRECTORY 관리 명령
1. `pwd` : 현재 `Directory`를 출력
2. `cd` : `Directory`를 이동
   * `ex) `cd '~', './', '..', '/usr', '-'`
   * `~` : `Home Directory`를 의미한다.
   * `.` : '현재 Directory`를 의미한다.
   * `..` : `상위 Directory`를 의미한다.
   * `/` : `최상위 Directory`로 이동한다.
   * `-` : `직전 Directory`로 이동한다.
4. 절대 경로 : `/` `~`, 절대 경로가 아니면 모두 상대 경로이다.
5. `ls` : `현재 Directory`의 파일 정보 출력
   * `-a` : 모든 파일을 출력 (.으로 시작하는 숨김 파일 포함)
   * `-l` : 파일 정보를 자세히 출력
   * `-al` : `a`와 `l` 명령어를 같이 적용하여 출력
6. `mkdir` : `Directory`를 생성한다.
   * `ex) : mkdir my_dir`
   * `-p` : 중간에 없는 `Directory`를 자동으로 생성한다.
7. `rmdir` : `Directory`를 삭제한다.



### 파일 관리 명령
1. `file` : 파일 정보를 출력 // Text file, ELF format 등
2. `stat` : 타임스탬프를 포함하는 파일의 정보를 출력 
   * `Access` : 파일의 내용을 읽을 때 갱신
   * `Modify` : 파일의 내용을 수정할 때 갱신
   * `Change` : 파일의 속성 또는 내용을 변경할 때 갱신
3. `touch` : 없던 파일을 생성 or 있는 파일의 타임 스탬프를 갱신
4. `cp` : `File`이나 `Directory`를 복사
   * `ex) hello.c hello_1.c`
   * `-i` : 파일 대상을 덮어 쓸지 물어봄
   * `-f` : 파일 대상이 열리지 않으면 강제로 지우고 다시 시도
   * `-f  Templates` : 복수의 소스 파일을 복사
   * `-r` : Templayes : `Directory`를 모두 복사, 이미 있을 경우 그 파일의 하위로 복사
5. `mv` : `File`이나 `Directory`를 이동하거나 이름을 변경
   * `ex) hello_1.c hello_2.c`
   *  `-f` : 무조건 덮어 씀
   * `주의 사항` : 원치 않게 `File`이나 `Dir`의 이름을 변경할 수 있다.
6. `rm` : `File`이나 `Directory`를 삭제한다.
   * `ex) mv MyDir/hello_1.c`
   *  `-r` : `Directory`를 삭제한다.
   *  `-f` `-rf` : 대상이 없거나 하는 이유로 실행에 실패해도 메세지를 출력하지 않음
7. `ln` : `File Link`를 만들어줌
   * `ex) ln -s /etc/issue myissue`
   *  `-s` : `Symbolic Link File`생성
   *  `Symbolic Link File`은 가리키는 주소의 `.exe`, `Dir`과 이어져 간편한 접근이 가능하다.
---
#
