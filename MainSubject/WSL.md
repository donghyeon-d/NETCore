# WSL

## 의미
- 윈도우에서 리눅스 환경을 돌릴 수 있게 만든 것
- 버전 1에서는 리눅스 커널을 직접 이용하는 것이 아니라, 대칭되는 명령어들로 변환해주는 정도였음
- 버전2에서는 하이퍼바이저 위에 리눅스 커널이 설치되어 리눅스 커널을 직접사용하는 느낌으로 됨. 물론, 가상환경에서 돌아가는 것이기 때문에 일반 머신에 깔려있는 리눅스보다 성능이 낮을 수밖에 없음.
- 파일시스템도 잘 구현되어서, 리눅스 내에서도 윈도우의 파일 시스템에 마운트 되어있어 직접 닿을 수 있음 (c드라이브 : 리눅스에서 /mnt/c)
- [참고](https://namu.wiki/w/UNIX/Microsoft%20Windows#s-6.2)

## 설치
### 설치 명령
- powershell에서 `wsl --install`
### 리눅스 배포판 설정
- 디폴트로 Ubuntu 배포판이 설치 됨
- 원하는 배포판으로 설치 : `wsl --install -d <배포판 이름>`
- 설치 가능한 배포판 목록 보기 : `wsl --list --online` ,  `wsl -l -o`
### 설치 후엔 Linux 사용자 정보를 설정해야 함
- [WSL 설치 참고](https://learn.microsoft.com/ko-kr/windows/wsl/install)

## **WSL - init에서 systemd**
- **System has not been booted with systemd as init system (PID 1). Can't operate.라는 오류 만남**
- mariadb-server 같은 거 daemon으로 돌리려할 때 에러남
- wsl이 init 버전으로 실행돼있어서 그럼. systemd로 실행해야 함
- [참고 : Linux: 51. WSL - init에서 systemd로 전환하는 방법](https://www.sysnet.pe.kr/2/0/13104?pageno=16)