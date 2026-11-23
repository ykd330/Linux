# Linux

---
# 리눅스 명령어
### DIRECTORY 관리 명령
- `pwd` : 현재 `Directory`를 출력
- `cd` : `Directory`를 이동
   * `ex) cd ~ ./ .. /usr - `
   * `~` : `Home` `Directory`를 의미한다.
   * `.` : `현재 Directory`를 의미한다.
   * `..` : `상위 Directory`를 의미한다.
   * `/` : `최상위 Directory`로 이동한다.
   * `-` : `직전 Directory`로 이동한다.
- 절대 경로 : `/` `~`, 절대 경로가 아니면 모두 상대 경로이다.
- `ls` : `현재 Directory`의 파일 정보 출력
   * `-a` : 모든 파일을 출력 (.으로 시작하는 숨김 파일 포함)
   * `-l` : 파일 정보를 자세히 출력
   * `-al` : `a`와 `l` 명령어를 같이 적용하여 출력
- `mkdir` : `Directory`를 생성한다.
   * `ex) : mkdir my_dir`
   * `-p` : 중간에 없는 `Directory`를 자동으로 생성한다.
- `rmdir` : `Directory`를 삭제한다.

- **예제 : Directory 관리**
- 자신의 홈 디렉터리로 이동 후 tdir1을 생성한다.
    * `cd ~`
    * `mkdir tdir1`
- /etc로 이동 후 ~/tdir1 아래에 tdir2를 생성한다.
    * `cd /etc`
    * `mkdir ~/tdir1/tdir2`
- 한번에 위에서 생성한 tdir2로 이동한다.
    * `cd ~/tdir1/tdir2`
- 홈 디렉터리로 이동 후 tdir1을 삭제한다.
    * `cd ~`
    * `rmdir ~/tdir1/tdir2`
    * `rmdir ~/tdir1`
---
### 파일 관리 명령
- `file` : 파일 정보를 출력 // Text file, ELF format 등
- `stat` : 타임스탬프를 포함하는 파일의 정보를 출력 
   * `Access` : 파일의 내용을 읽을 때 갱신
   * `Modify` : 파일의 내용을 수정할 때 갱신
   * `Change` : 파일의 속성 또는 내용을 변경할 때 갱신
- `touch` : 없던 파일을 생성 or 있는 파일의 타임 스탬프를 갱신
- `cp` : `File`이나 `Directory`를 복사
   * `ex) hello.c hello_1.c`
   * `-i` : 파일 대상을 덮어 쓸지 물어봄
   * `-f` : 파일 대상이 열리지 않으면 강제로 지우고 다시 시도
   * `-f  Templates` : 복수의 소스 파일을 복사
   * `-r` : Templayes : `Directory`를 모두 복사, 이미 있을 경우 그 파일의 하위로 복사
- `mv` : `File`이나 `Directory`를 이동하거나 이름을 변경
   * `ex) hello_1.c hello_2.c`
   *  `-f` : 무조건 덮어 씀
   * `주의 사항` : 원치 않게 `File`이나 `Dir`의 이름을 변경할 수 있다.
- `rm` : `File`이나 `Directory`를 삭제한다.
   * `ex) mv MyDir/hello_1.c`
   *  `-r` : `Directory`를 삭제한다.
   *  `-f` `-rf` : 대상이 없거나 하는 이유로 실행에 실패해도 메세지를 출력하지 않음
- `ln` : `File Link`를 만들어줌
   * `ex) ln -s /etc/issue myissue`
   *  `-s` : `Symbolic Link File`생성
   *  `Symbolic Link File`은 가리키는 주소의 `.exe`, `Dir`과 이어져 간편한 접근이 가능하다.
**예제 : File 관리**
1. /etc 디렉터리를 통째로 홈 디렉터리에 복사한다.
    * `cp -r /etc ~`
2. 홈 디렉터리에 복사한 etc 디렉터리의 이름을 my_etc로 변경한다.
    * `mv etc my_etc`
3. 홈 디렉터리에 my_backup 디렉터리를 생성한다.
    * `mkdir my_backup`
4. my_etc를 my_backup으로 이동한다.
    * `mv my_etc my_backup`
5. my_backup 디렉터리를 삭제한다.
    * `rm -rf my_backup`
---
### 텍스트 파일 보기 명령
- `cat` : 텍스트 파일의 내용을 화면에 출력 / 서로 다른 파일을 연결 시킬 때 사용할 수 있다. (Re Direction [ `>` ]) 
   * `ex) cat /etc/services`
- `more` / `less` : 텍스트 파일의 내용을 화면에 한 페이지씩 출력
   * `more' : 텍스트 파일의 내용을 한 페이지씩 출력함
   * `less` : `more`의 기능에 마우스 커서로 `상 하`로 이동 가능한 기능이 추가됨
- `head` / `tail` : 텍스트 파일의 `시작` / `끝` 부분을 출력
   * `ex) head -5 /etc/profile / tail -20 /etc/profile`
   * `-[N]` : (head)첫 `N`줄 출력 / (tail)끝 `N`줄 출력 (`N` 생략시 기본 10줄)
---
# 사용자와 그룹
### 사용자와 그룹
1. `Linux`는 여러 사람이 동시에 시스템에 접근 가능한 `multi user OS`
   * `관리자` : 모든 기능을 사용할 수 있는 사용자
   * `시스템 사용자` : 특정 기능만 접근하는 사용자
   * `일반 사용자` : login과 같은 수단으로 시스템에 접근하여 사용하는 사용자
   * ### Group
   * 여러 사용자를 묶어서 관리할 목적으로 생성
     - `사용자 이름` : `사용자 암호` : `UID` : `GID` : `설명` : `사용자 홈 디렉터리` : `사용자 로그인 쉘`
     - `사용자 암호` : 암호화된 암호 : `x`일 경우 `/etc/shadow`에 있음 (관리자 권환`sudo` 사용해야함)
     - `UID`는 사용자의 고유 번호 : `0 : 관리자` `1 ~ 999 : 시스템 사용자` `1000 이상 : 일반 사용자` (시스템에 따라 값이 달라질 수 있음)
     - `GID`는 사용자가 속한 `주 그룹`의 고유 번호
        * 모든 사용자는 하나의 `주 그룹`과 복수의 `보조 그룹`에 포함됨
        * 사용자가 생성한 모든 파일은 `주 그룹`이 소유함
        * `보조 그룹`은 특정 리소스에 대한 접근 권한을 공유하는데 사용
     - 그룹의 관리는 관리자의 권한으로 처리
     - `그룹에 속한 사용자들` 해당 그룹을 보조 그룹으로 하는 사용자들을 `,`로 구분
  * # 과제 1. willtek이 속한 보조 그룹을 찾기
    * ### 명령어로 찾기
     - `id <User>` / `groups <User>` : `<User>`가 속한 모든 그룹 목록 출력
        * `-g` : 사용자가 속한 주 그룹만 출력
        * `-Gn willtek | sed "s/\b$(id -gn <User>)\b//g" | xargs` : 사용자가 속한 보조 그룹만 출력
        * `id` 출력 값 : `uid=1000(willtek)gid=1000(willtek)groups=1000(willtek),4(adm),20(dialout),24(cdrom),27(sudo),29(audio),44(video),46(plugdev),60(games),100(users),102(input),105(render),110(netdev),115(lpadmin),993(gpio),994(i2c),995(spi)`

    * ### group 파일로 찾기
     - `grep "<User>:" /etc/group` : 주 그룹만 출력
        * 출력 값 : `willtek:x:1000:`
     - `grep "<User>" /etc/group` : 보조 그룹만 출력
        * 출력 값 : 
         -`adm:x:4:willtek`
         -`dialout:x:20:willtek`
         -`cdrom:x:24:willtek`
         -`sudo:x:27:willtek`
         -`audio:x:29:pulse,willtek`
         -`video:x:44:vnc,willtek`
         -`plugdev:x:46:willtek`
         -`games:x:60:willtek`
         -`users:x:100:willtek`
         -`input:x:102:lightdm,willtek`
         -`render:x:105:vnc,willtek`
         -`netdev:x:110:willtek`
         -`spi:x:995:willtek`
         -`i2c:x:994:willtek`
         -`gpio:x:993:willtek`
         -`lpadmin:x:115:willtek`


