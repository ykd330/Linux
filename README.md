# Linux

## 1과. Linux Command

* `terminal` : `shell`의 입출력을 담당한다.
* `shell` : `Linux OS`에 명령을 전달하기 위한 명령어 해석기
  * `shell` 하나 당 `terminal` 하나를 사용한다.

#### 명령어 사용

* 명령 프롬프트 구조
  * 예시: `willtek@raspberrypi:~/work $ ls -l`
  * 계정 이름 : `willtek`
  * 시스템 이름 : `raspberrypi`
  * 작업 위치 : `~/work`
  * 프롬프트 기호 : `$` (일반 사용자) | `#` (관리자)
  * 명령어 : `ls -l`

#### 명령어 사용 매뉴얼

* `man` : 명령어나 함수 등 명령의 매뉴얼을 출력한다.
  * `-k` : 명령어가 포함된 페이지의 리스트를 출력
  * `-N` : `N`번 섹션에 있는 명령의 매뉴얼 페이지 출력

#### 매뉴얼 페이지 구성

* `Name` : 명령에 대한 간략한 설명
  * 예시: `ls - list directory contents`
* `Synopsis` : 명령어 사용 형식
  * 예시: `ls [OPTION]... [FILE]...`
* `Description` : 명령어 세부 내역 기술
  * 예시: `List information about the FILEs (the curren... -a, --all do not ignore entries starting with.`

---

## 1. Linux 기본 명령

#### 외부 명령 vs 쉘 내장 명령

* `which` : 명령어가 저장된 위치를 출력 (외부 명령일 경우 사용)
* `help` : `which`로 명령어의 위치를 확인할 수 없을 때 사용 / 명령어의 사용법을 출력
* `type` : `shell` 내장 함수일 경우 `<> is a shell builtin` 출력 | 아닐 경우 명령의 주소 출력

#### Directory 관리 명령

* `pwd` : 현재 `Directory`를 출력
* `cd` : `Directory`를 이동
  * 예시: `cd ~ ./ .. /usr -`
  * `~` : `Home` `Directory`
  * `.` : 현재 `Directory`
  * `..` : 상위 `Directory`
  * `/` : 최상위 `Directory`
  * `-` : 직전 `Directory`
* **절대 경로** : `/`, `~`로 시작하는 경로 (절대 경로가 아니면 모두 상대 경로)
* `ls` : 현재 `Directory`의 파일 정보 출력
  * `-a` : 모든 파일 출력 (`.`으로 시작하는 숨김 파일 포함)
  * `-l` : 파일 정보를 자세히 출력
  * `-al` : `-a`와 `-l` 옵션을 함께 적용하여 출력
* `mkdir` : `Directory` 생성
  * 예시: `mkdir my_dir`
  * `-p` : 중간에 없는 `Directory`를 자동으로 생성
* `rmdir` : `Directory` 삭제

---

#### 예제 : Directory 관리

1. 자신의 홈 디렉터리로 이동 후 `tdir1`을 생성한다.
   * `cd ~`
   * `mkdir tdir1`
2. `/etc`로 이동 후 `~/tdir1` 아래에 `tdir2`를 생성한다.
   * `cd /etc`
   * `mkdir ~/tdir1/tdir2`
3. 한 번에 위에서 생성한 `tdir2`로 이동한다.
   * `cd ~/tdir1/tdir2`
4. 홈 디렉터리로 이동 후 `tdir1`을 삭제한다.
   * `cd ~`
   * `rmdir ~/tdir1/tdir2`
   * `rmdir ~/tdir1`

---

#### 파일 관리 명령

* `file` : 파일 정보 출력 (Text file, ELF format 등)
* `stat` : 타임스탬프를 포함하는 파일 정보 출력
  * `Access` : 파일 내용을 읽을 때 갱신
  * `Modify` : 파일 내용을 수정할 때 갱신
  * `Change` : 파일 속성 또는 내용을 변경할 때 갱신
* `touch` : 빈 파일 생성 또는 기존 파일의 타임스탬프 갱신
* `cp` : `File`이나 `Directory` 복사
  * 예시: `cp hello.c hello_1.c`
  * `-i` : 덮어쓸지 여부 확인
  * `-f` : 파일이 열리지 않으면 강제로 지우고 재시도
  * `-f Templates` : 복수의 소스 파일 복사
  * `-r` : `Directory` 전체 복사 (이미 존재할 경우 하위 디렉터리로 복사)
* `mv` : `File`이나 `Directory` 이동 또는 이름 변경
  * 예시: `mv hello_1.c hello_2.c`
  * `-f` : 무조건 덮어씀
  * **주의 사항** : 원치 않게 `File`이나 `Dir` 이름이 변경될 수 있음
* `rm` : `File`이나 `Directory` 삭제
  * 예시: `rm MyDir/hello_1.c` *(원문 표기 유지)*
  * `-r` : `Directory` 삭제
  * `-f` / `-rf` : 대상이 없거나 실패해도 에러 메시지 미출력
* `ln` : `File` 링크 생성
  * 예시: `ln -s /etc/issue myissue`
  * `-s` : `Symbolic Link File` 생성
  * 가리키는 주소의 `.exe`, `Dir`과 이어져 간편한 접근 가능

---

#### 예제 : File 관리

1. `/etc` 디렉터리를 통째로 홈 디렉터리에 복사한다.
   * `cp -r /etc ~`
2. 홈 디렉터리에 복사한 `etc` 디렉터리의 이름을 `my_etc`로 변경한다.
   * `mv etc my_etc`
3. 홈 디렉터리에 `my_backup` 디렉터리를 생성한다.
   * `mkdir my_backup`
4. `my_etc`를 `my_backup`으로 이동한다.
   * `mv my_etc my_backup`
5. `my_backup` 디렉터리를 삭제한다.
   * `rm -rf my_backup`

---

#### 텍스트 파일 보기 명령

* `cat` : 텍스트 파일 내용을 화면에 출력 / 서로 다른 파일을 연결할 때 사용 (Redirection [`>`])
  * 예시: `cat /etc/services`
* `more` / `less` : 텍스트 파일 내용을 화면에 한 페이지씩 출력
  * `more` : 한 페이지씩 출력
  * `less` : `more` 기능에 상·하 이동 등 탐색 기능 추가
* `head` / `tail` : 텍스트 파일의 시작 / 끝 부분 출력
  * 예시: `head -5 /etc/profile` / `tail -20 /etc/profile`
  * `-[N]` : `head`는 첫 `N`줄, `tail`은 끝 `N`줄 출력 (`N` 생략 시 기본 10줄)

---

## 2. 사용자와 그룹

### 사용자와 그룹 개요

1. `Linux`는 여러 사람이 동시에 시스템에 접근 가능한 `multi user OS`
   * **관리자** : 모든 기능을 사용할 수 있는 사용자
   * **시스템 사용자** : 특정 기능만 접근하는 사용자
   * **일반 사용자** : 로그인 등을 통해 시스템에 접근하여 사용하는 사용자

---

#### Group

* 여러 사용자를 묶어서 관리할 목적으로 생성
  * 계정 필드 구성 : `사용자 이름` : `사용자 암호` : `UID` : `GID` : `설명` : `사용자 홈 디렉터리` : `사용자 로그인 쉘`
  * **사용자 암호** : 암호화된 암호 (`x`일 경우 `/etc/shadow`에 저장, `sudo` 권한 필요)
  * `UID` : 사용자 고유 번호 (`0` : 관리자 | `1 ~ 999` : 시스템 사용자 | `1000 이상` : 일반 사용자 — 시스템에 따라 번호 수가 변화할 수 있음)
  * `GID` : 사용자가 속한 `주 그룹` 고유 번호
    * 모든 사용자는 하나의 `주 그룹`과 복수의 `보조 그룹`에 포함됨
    * 사용자가 생성한 모든 파일은 `주 그룹`이 소유함
    * `보조 그룹`은 특정 리소스에 대한 접근 권한 공유에 사용
  * 그룹 관리는 관리자 권한으로 처리
  * **그룹에 속한 사용자들** : 해당 그룹을 보조 그룹으로 가지는 사용자들을 `,`로 구분

---

#### 과제 1. `willtek`이 속한 보조 그룹 찾기

* **`id` 명령으로 찾기**
  * `id <User>` / `groups <User>` : `<User>`가 속한 모든 그룹 목록 출력
    * `-g` : 사용자가 속한 주 그룹만 출력
    * `id -Gn willtek | sed "s/\b$(id -gn <User>)\b//g" | xargs` : 사용자가 속한 보조 그룹만 출력
    * `id` 출력 값 :
      `uid=1000(willtek)gid=1000(willtek)groups=1000(willtek),4(adm),20(dialout),24(cdrom),27(sudo),29(audio),44(video),46(plugdev),60(games),100(users),102(input),105(render),110(netdev),115(lpadmin),993(gpio),994(i2c),995(spi)`

* **`grep` 명령으로 찾기**
  * `grep "<User>:" /etc/group` : 주 그룹 관련 항목 출력
    * 출력 값 : `willtek:x:1000:`
  * `grep "<User>" /etc/group` : 보조 그룹 관련 항목 출력
    * 출력 값 :
      * `adm:x:4:willtek`
      * `dialout:x:20:willtek`
      * `cdrom:x:24:willtek`
      * `sudo:x:27:willtek`
      * `audio:x:29:pulse,willtek`
      * `video:x:44:vnc,willtek`
      * `plugdev:x:46:willtek`
      * `games:x:60:willtek`
      * `users:x:100:willtek`
      * `input:x:102:lightdm,willtek`
      * `render:x:105:vnc,willtek`
      * `netdev:x:110:willtek`
      * `spi:x:995:willtek`
      * `i2c:x:994:willtek`
      * `gpio:x:993:willtek`
      * `lpadmin:x:115:willtek`

---

## 3. 파일 접근 권한

#### 파일 종류

* `-` : 정규 파일 (실제 존재하는 파일)
* `d` : `Directory` 파일
* `l` : `Symbolic Link` 파일
* `c` : 문자 디바이스 파일
* `b` : 블록 디바이스 파일
* `p` : 파이프
* `s` : 소켓

* `ls -l /var/log/wtmp`
  -> `-` (파일 종류) `rw-rw-r--` (접근 권한) `1` `root` (소유자) `utmp` (소유 그룹)

---

#### 접근 권한

* `r` : (non dir) 읽기 가능 | (dir) 파일 목록 보기 가능
* `w` : (non dir) 쓰기 가능 | (dir) 파일 생성 및 삭제 가능
* `x` : (non dir) 실행 가능 | (dir) 진입 가능
* `-` : 해당 기능 불가능
  * `rwx|rwx|rwx`와 같이 표시 : `1. user` `2. group` `3. other`

---

#### 파일 보안 명령

* `chmod` : 파일의 접근 권한을 변경
  * `8진 모드` : 접근 권한 전체를 한 번에 변경
    * 8진 -> 2진 (`111` : `rwx`) : (`110` : `rw-`) : (`100` : `r--`)
  * `기호 모드` : 접근 권한 일부를 선택적으로 변경
    * `(a : 모든 사용자)` : `(u : 소유자)` : `(g : 소유 그룹)` : `(o : 나머지 사용자)` || `(+ : 추가)` : `(- : 제거)`
    * `a-x` : `(a, u, g, o)(+, -)(r, w, x)`
* `chown` : 소유자 및 소유 그룹 변경
* `chgrp` : 소유 그룹을 변경
* `umask` : 파일 생성 시 특정 접근 권한을 비활성화 (`process` 의존적)
  * **실수로 불필요하거나 위험한 권한의 활성화를 방지**
  * `umask` 값을 출력하거나 수정할 수 있는 명령
  * 모든 `process`는 `umask` 값을 가지고 있음
    * `umask` : `0022` (`shell`이 가지고 있는 `umask` 값)
  * `umask` : `8진수` | `0022` -> `0` (특별 권한) `022` (접근 권한 : `user` `group` `other`) -> 여기선 `group`과 `other`의 `w` 접근 권한 비활성화
  * **예제 실행 결과**
    * `willtek@raspberrypi:~ $ ls -l aaa`
    * `-rw-r--r-- 1 willtek willtek 0 Nov 23 23:20 aaa`
    * `willtek@raspberrypi:~ $ umask 0002`
    * `willtek@raspberrypi:~ $ umask`
    * `0002`
    * `willtek@raspberrypi:~ $ touch bbb`
    * `willtek@raspberrypi:~ $ ls -l bbb`
    * `-rw-rw-r-- 1 willtek willtek 0 Nov 23 23:20 bbb`
      * `bbb`에선 `umask` 값이 `0002` (기존의 `0022`와 비교해서 `group` 접근 권한 중 `w`를 비활성화시키지 않음)이므로 접근 권한은 `-` (파일의 종류) | `rw-rw-r--` (파일 접근 권한)으로 출력
* `grep` : 파일 검색 명령
  * 예시: `grep root /etc/passwd` : `/etc/passwd`에서 `root`를 포함한 행 출력
  * `-v` : 기존 명령과 반대로 포함하지 않는 행을 출력
  * 예시: `grep root /etc/*` : `/etc` 밑에 있는 모든 파일 검색 (`*` : 현재 `Directory`의 모든 파일을 의미)
  * `-i` : 대소문자를 구분하지 않음
  * `-w` : 정확히 일치하는 단어 검색
  * `-c` : 파일 별 패턴을 포함한 행의 수를 출력
  * `-r` : 하위 `Directory`도 모두 검색
  * `-rn` : 행 번호도 출력

---

#### Standard I/O와 Redirection

**표준 입출력 : `process`가 외부와 데이터를 교환하기 위한 통로**
* `표준 입력 | 표준 출력 | 표준 에러` (실제 장치는 상황에 따라 다름)
* `표준 입출력`은 `부모`에게 상속 받음
* `ls` -> `ls` 명령을 `표준 입력`으로 입력
* `desktop Documents...` : 명령의 결과를 `표준 출력`으로 출력
* `ls xxx` : `ls xxx` 명령을 `표준 입력`으로 입력
* `ls: cannot access 'xxx': ...` : 명령의 결과를 `표준 에러`로 출력

**Redirection : `표준 입출력`을 특정 파일로 재지정함**
* `ls -l > ls.txt` : 명령의 결과를 표준 출력 대신 `ls.txt`로 출력 (기존 내용에 덮어씀)
* `echo "test failed" >> log.txt` : `log.txt`에 추가됨 (기존 내용에 이어서 작성)
* `cat` : 표준 입력으로 받은 내용을 출력
  * `cat < ls.txt` : `표준 입력`으로 `ls.txt`를 사용
* `cat < log.txt` : 부모 `shell` 파일을 읽음
* `cat log.txt` : `shell`이 파일을 읽음
* `0 : 표준 입력` `1 : 표준 출력` `2 : 표준 에러` `& : 입출력 + 에러`
  * `2>` : 표준 에러를 특정 파일로 재지정
  * `2>&1` : 에러를 정상 출력과 같은 파일에 출력

**Pipe : 앞 명령의 표준 출력을 뒤 명령의 표준 입력으로 전달**
* `ls -l /etc | grep conf` : `conf`가 있는 파일을 찾음
* `ls -l /etc | grep conf | less` : `conf`가 있는 파일을 `less`로 봄
* `cat /etc/passwd | grep sys` : `passwd`에서 `sys`가 포함된 행 출력
* `cat /etc/passwd | grep sys | grep -v run` : `passwd`에서 `sys`가 포함되고 `run`이 포함되지 않는 행 출력

---

#### 예제 : 파일 및 텍스트 검색

1. `/etc` 디렉터리에서 (하위 디렉터리 제외) 접근 권한이 `755`인 디렉터리를 모두 출력하라
   * `ls -l /etc | grep ^drwxr-xr-x`
2. `/etc` 디렉터리에서 (하위 디렉터리 제외) 파일명에 `bash`와 `comp`를 동시에 포함한 파일 (디렉터리도 포함)을 모두 출력하라
   * `ls /etc | grep bash | grep comp` (`-R`을 포함하면 하위 디렉터리를 포함함)
3. `/etc/services` 파일에서 `tcp`와 `daemon`은 포함하지만 `service`는 포함하지 않는 행을 모두 출력하라
   * `cat /etc/services | grep tcp | grep daemon | grep -v service`
4. 저장된 커널 메시지를 출력하는 `dmesg` 명령의 결과 중 `enabled`를 포함한 행을 모두 출력하라
   * `dmesg | grep enabled`

---

#### 과제 2. `glob` 문자에 대해 조사하기 [`*`, `?`, `[]`]

* 의미 : 리눅스 운영체제에서 한 번에 여러 개의 파일을 찾을 때 사용해온 패턴 매칭 기법
* 쓰임새 :
  * `*` : 길이와 상관없이 모든 문자열과 부합한다.
    * `a*` : `a`로 시작하는 모든 파일
  * `?` : `?` 위치의 글자와 1:1로 매칭된다.
    * `a?` : `ab`, `ac`, `a0` 등 (단, `acv`와 같은 문자열은 매칭되지 않는다.)
    * `a??` : `avx`, `axc`, `a01` 등
    * `?` 패턴은 여러 개 사용할 수 있다.
  * `**` : `Dir` 사이에 사용되면 해당 위치에 있는 모든 `Dir`과 매칭된다.
    * `logs/**/X.log` : `logs/.../X.log`가 있다면 중간 `Dir`의 이름과 개수는 무시할 수 있다.
    * `logs/**/X.log` -> `logs/bin/X.log`, `logs/a/b/X.log` 등
  * `{}` : 여러 문자 패턴을 하나로 통합할 수 있다.
    * `.{jpg,JPG}` -> 확장자가 `jpg`인 파일과 `JPG`인 파일을 동시에 찾을 수 있음
  * `[]` : 문자의 범위를 기준으로 파일을 찾을 때 사용
    * `*[aeiou]*` -> `a`, `e`, `i`, `o`, `u`가 들어간 파일 찾기
    * `[A-Z]*` -> 대문자 이름으로 시작하는 파일 찾기
  * `()` : `?`, `*` 바로 뒤에 `()`를 사용하면 선택지를 제한한다.
    * `?(ab|cd)` -> `ab` 또는 `cd` 문자열, `null` 문자열과 매칭된다.
    * `*(ab|cd)` -> `ab`, `abab`, `cdaf`와 같이 포함된 문자열이 시작하는 파일과 매칭된다.

---

## 2과. Shell Script

* `shell` : `User`와 `Linux OS` 사이의 인터페이스 역할을 하는 프로그램
  * 윈도우의 CMD와 비슷하지만 더 강력한 기능을 제공함
  * `shell`에는 `sh`, `dash`, `bash`, `ksh`, `csh` 등 다양한 쉘이 있다.
  * `sh` : `system`용 `shell`로 다른 `shell`을 `Symbolic Link`하고 있음
  * `dash` : `bash`보다 기능은 적지만 실행 속도가 빠르고 메모리 사용량이 적음 -> `User`보다는 `System`용에 적합
  * `bash` : `User`가 사용하기 적합한 `shell`
  * `shell`은 스크립트 언어로 작성된 프로그램을 실행시킬 수 있다.
    * 컴파일 언어 : `C`, `C++` 등 `source`를 `compile`해서 기계어로 변환 후 실행 => `system`에 종속적
    * 스크립트 언어 : `shell script`, `python` 등 `source`를 `인터프리터`가 실행 => `system`에 비종속적

---

#### 실습 : Shell script 작성 및 실행

**`hello.sh` 파일을 생성**

* `#!/bin/bash` : `#!`은 스크립트를 실행할 프로그램 `Shell`의 절대 경로를 지정 (없을 경우 지정된 `shell`로 자동 지정)
* `#print messages` : 주석 처리
* `echo "Hello! Shell script"` : `echo`(명령어) `"Hello! Shell script"` (출력 내용)
* `exit 0` : 값을 반환하고 `shell` 종료
  * `exit`가 없다면 마지막에 실행된 명령의 값을 반환하고 종료

**실행 권한 부여 후 실행**

* `chmod a+x hello.sh`
* `./hello.sh`
* `Hello! Shell script`

**실행 결과**

* `Hello! Shell script`

---

#### 예제 : 변수

**변수는 기본적으로 문자열로 저장 / 선언이 없어도 사용 가능**

* `name=linux` : `name`에 `"linux"` 대입
  * 대입 연산과 변수 사이에 공백이 있으면 안 됨
* `echo name: $name`
  * `name` : `name` 출력, `$name` : `name` 변수의 값이 출력
* `echo name: ${name}`
  * `echo name: $name`과 동일
* `name=programming`
  * `name`에 `programming` 대입
* `echo name: $name`
  * `name` 값 `programming` 출력
* `echo course: $course`
  * `course:`만 출력

---

#### 예제 : Quoting

`var=hello`

* `touch aaa bbb` : 파일 `aaa`, `bbb` 생성
* `touch "aaa bbb"` : 파일 `aaa bbb` 생성
* `echo $var` : `hello` 출력
* `echo "$var"` : `hello` 출력 + `$`, `` ` ``, `\`를 특수 용도로 인식
* `ls /etc/issue*` : `issue`로 시작하는 파일 실행
* `ls "/etc/issue*"` : 에러 발생 : `*`이 특수 기호가 아닌 문자로 인식
* `touch 'ccc ddd'` : `ccc ddd` 파일 생성
* `echo '$var'` : `$var` 출력 됨 (`''`는 모든 특수 기호를 문자로 인식함)
* `ls '/etc/issue*'` : 에러

---

#### ESCAPING

1. `\` : 문자의 특수 기능을 제거
2. `\` : 문자에 특수 기능을 부여

**특수 기능 제거 예제**

* `echo \$var` : `$var` 출력 (`$`의 특수 기능이 제거됨)
* `echo \\$var` : `\hello` 출력 (`\`의 특수 기능이 제거됨)
* `echo \"$var\"` : `"hello"` 출력 : `"`의 특수 기능이 제거됨
* `echo \'$var\'` : `'hello'` 출력 : `'`의 특수 기능이 제거됨
* `echo \'pwd\'` : `'pwd'` 출력
* `echo \a\b\c\d` : `abcd` 출력
* `echo "\a\b\c\d"` : `\a\b\c\d` 출력

**특수 기능 부여**

* `echo -e` 같은 특정 명령과 ASCII에서 적용
* `\n` : 줄 바꿈
* `\r` : 리턴
* `\t` : 탭
* `\v` : 버티컬 탭
* `\b` : 백스페이스
* `\a` : 부저
* `\xHH` : 16진수
* `\0nnn`, `\nnn` : 8진수

**특수 기능 부여 예제**

* 문자 처리는 `echo` / ASCII 처리는 `shell`이 담당
* `echo 111\n222\t333` : `\`는 무시되고 출력
* `echo "111\n222\t333"` : `\`가 문자 취급되어 같이 출력
* `echo -e "111\n222\t333"` : `\n`, `\t`에 특수 기능이 부여됨
* `echo -e "\x31\x32\x33"` : `\x`로 16진수 표기
* `echo -e '\x31\x32\x33'` : `\x`로 16진수 표기
* `echo $'\x31\x32\x33'` : `$' '`는 ASCII로 출력해줌

---

#### 실습 : 변수에 문자열 대입

* `name="linux"`
* `course="expert"`

#### linux expert

* `var="$name $course"`
* `echo $var`

#### $linux \expert

* `var="\$$name \\$course"`
  * 특수 문자 `$`의 기능을 제거하고 `$`가 출력되도록 함 -> `\$$name` -> `$linux`
  * 특수 문자 `\`의 기능을 제거하고 `\`가 출력되도록 함 -> `\\$course` -> `\expert`
* `echo $var`

#### $$linux \\expert

* `var="\$\$$name \\\\$course"`
  * 특수 문자 `$`의 기능을 제거하여 출력함 `\$\$$name` -> `$$linux`
  * 특수 문자 `\`의 기능을 제거하여 출력함 `\\\\$course` -> `\\expert`
* `echo $var`

#### experted linux

* `var="${course}ed $name"`
  * 변수 `course`의 값을 꺼냄 -> `expert` -> `${course}` 자리에 대입 -> `experted`
* `echo $var`

#### 실행 결과

* `linux expert`
* `$linux \expert`
* `$$linux \\expert`
* `experted linux`

---

#### 변수 내보내기

* `부모`가 `자식`에게 변수를 전달
* `export` : 내보내기 변수를 설정함
  * `export name=linux` : 설정하면서 변수에 값 대입도 가능
  * 내보내기 변수로 설정되고 `자식`이 실행되면 이후에 `부모`의 변수 값이 변화하더라도 `자식`의 값은 변하지 않는다. (처음 받은 값을 유지)
  * 내보내기 변수로 설정되더라도 `자식`이 가진 변수의 변화는 `부모`가 가진 변수에 영향을 주지 않는다. (다만 `자식`이 또 다른 `자식`을 만들 경우 환경 변수가 그대로 넘어감)
  * 실행되는 시점엔 동일한 변수이지만 실행 중인 시점부터는 변수의 값이 변하더라도 서로 영향을 주지 않는다.

---

#### 지역 변수와 환경 변수

* 현재 `shell`에서 만든 변수는 `지역 변수`, `export`하면 `환경 변수`
* `set` : 모든 변수와 함수를 출력 (`pipe` + `more` 사용하여 확인하면 편리하다.)
* `env` : 환경 변수만 출력
* `unset` : 변수를 제거함 -> `unset PATH`를 실행하면 `PATH`가 사라져 외부 명령을 사용할 수 없게 된다.

**주요 변수**

* **주요 환경 변수**
  * `HOME` : 현재 사용자의 홈 `Directory`
  * `PATH` : 실행할 명령을 찾을 `Directory` 목록
  * `USER` : 사용자의 이름
  * `PWD` : 현재 `Directory`
* **주요 shell 변수**
  * `PS1` : `Shell` 명령 프롬프트 형식
  * `PS2` : 2차 명령 프롬프트 -> 명령을 `\`로 이어서 입력했을 때 표시
  * `RANDOM` : `0 ~ 32767` 사이의 난수
  * `UID` : 현재 사용자의 ID
  * `PPID` : 부모의 프로세스 ID

* `source` : 스크립트가 현재 쉘에서 실행된다.
* **특수 변수**
  * `$#` : 넘어온 옵션과 인자의 개수
  * `$0` : 명령 저장
  * `$1`, `$2` : 넘어온 인자를 순서대로 저장함
  * `$$` : 현재 프로세스의 ID
  * `$?` : 직전 명령의 반환 값을 저장 (명령 수행에 성공하면 `0` 반환 / 실패 시 `1` 이상의 값 반환)

---

#### 과제 1. 명령 치환(command substitution)에 대해 조사 [`` `...` ``, `$(...)`]
* 특정 명령어를 먼저 실행한 후 그 표준 출력 결과를 다른 명령어의 인자나 변수 값으로 끼워 넣는 기능 ( = 명령어 출력 결과를 문자열로 반환한다 )
  * 사용 방법 : `$(명령어)` -> `Today=$(date +%F)` | `ls -la $(pwd)`
  * `"$(...)"` : `줄 바꿈`이나 `공백`이 있더라도 하나의 문자열로 유지
  * `$(...)` (따옴표 미사용 시) : `줄 바꿈`이나 `공백`을 기준으로 나뉘어 여러 인자가 전달될 수 있음 (와일드카드가 확장될 수 있다.)
  * `공백`이나 `줄 바꿈`이 있는 파일 명을 결과로 넘기면 문자열이 쪼개질 수 있으니 주의해야 한다.

#### 과제 2. 받은 인자에서 소문자들만 대문자로 바꾸어 출력하는 스크립트
* `#!/bin/bash`
* `echo $1 | tr [:lower:] [:upper:]`
* `exit 0`

---

## 3과. 응용 프로그램 개발

#### GNU 툴체인
* 실행 파일을 만드는데 필요한 툴들의 집합
 - `Linux`는 `GNU` 프로젝트에서 만든 `GNU 툴체인`을 사용
 
**GNU 툴체인의 주요 구성 요소**
* `GNU Binary Utilities` : 어셈블러, 링커 등의 프로그래밍 툴들의 모음
* `GNU Compiler Collection (GCC)` : 선행처리기, 컴파일러 등의 모음
* `GNU C 라이브러리 (glibc)` : 응용 프로그램과 커널 간 인터페이스를 제공하는 API
* `GNU make` : 빌드 자동화 유틸리티

**GNU 툴체인을 이용한 빌드 과정**
* `선행처리(preprocess)` : `cpp` : `#include` `#define` 등 처리 : `.c` -> `.i`
* `컴파일(compile)` : `cc1` : 어셈블리어 파일 생성 : `.i` -> `.s`
* `어셈블(assemble)` : `as` : 오브젝트 파일 생성 : `.s` -> `.o`
* `링크(link)` : `ld` : `elf`형식의 실행 파일 생성 `.o` -> 실행 파일
* `gcc` 명령은 위 과정을 관리

**cross 툴체인**
* `native` : 빌드하는 기기와 실행하는 기기가 동일
  - `Build : PC -> Run : PC` 등
* `cross` : 빌드하는 기기와 실행하는 기기가 다름
  - `Build : PC -> Run : Board` 등

**cross 툴체인 선택**
* 누군가가 이미 빌드한 툴체인 사용
  - 현재 환경을 지원하도록 설정이 되어 있어야 함
* `Buildroot` `Yocto` 등의 빌드 시스템을 사용
* 직접 빌드
  - crosstool-NG 프로그램 사용 / 각각의 구성 요소를 직접 빌드

**실습 : raspberryPi GNU gcc compile**
* `aarch64-linux-gnu-gcc func.c main.c`
* `ls .`
  - -> a.out  func.c  main.c
* `./a.out`
  - -> `main: Hello!` `func: Hello!`
