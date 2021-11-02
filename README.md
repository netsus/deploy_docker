설치 
 1. 우분투 에서, docker 설치
  1) 최신 패키지 리스트 업데이트
     sudo apt update
  2) docker 다운로드를 위해 필요한 https 관련 패키지 설치
     sudo apt install apt-transport-https ca-certificates curl softwareproperties-common
  3) docker repository 접근을 위한 GPG key 설정
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  4) docker repository 등록
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  5) 등록한 docker repository 까지 포함하여 최신 패키지 리스트 업데이트
     sudo apt update
  6) docker 설치
     sudo apt install docker-ce
  7) docker 실행 중임을 확인
     sudo systemctl status docker

 2. sudo 명령 없이 docker 명령어 사용하기 설정
  1) 현 사용자(ubuntu) ID 를 docker group 에 포함
     sudo usermod -aG docker ${USER}
  2) 터미널 끊고, 다시 ssh 로 터미널로 접속 (로그인을 다시 하는 것임)
  3) 현 ID 가 docker group 에 포함되어 있는지를 확인하는 명령 (docker 가 리스트에 나오면 됨)
     id -nG
  4) 이제 sudo 없이 docker 명령을 바로 내릴 수 있음
     docker

 3. 우분투 에서, docker‑compose 설치
  1) docker‑compose 설치
     sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/dockercompose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  2) 실행 권한 주기
     sudo chmod +x /usr/local/bin/docker-compose
  3) 다음 명령 실행시 버전 확인이 가능하면, 성공
     docker-compose --version


docker 기본 개념
 1. docker : 컨테이너 기반의 가상화 플랫폼. 컨테이너 상에 서버를 셋업 함으로써, 언제든 해당 환경을 불러올 수 있다.
 2. docker image : docker 컨테이너를 생성하기 위한 명령들(스크립트의 모음). 스크립트들은 layer처럼 쌓여있다.
 3. docker container : docker image가 리눅스 컨테이너 형태로 실행한 상태(inxtance)를 의미


 docker search
 1. docker search --limit=5 [이미지 이름] : 이미지 이름 검색 결과에 대해 상위 5개만 보여줘라
     ex) docker search --limit=5 ubuntu
    1) 이미지이름 뒤에는 이미지이름[:태그] 형식으로 버전정보를 쓸 수 있다. (default는 :latest로 최신버전 설치됨)
    --> 태그는 hub.docker.com 사이트에서 확인 가능.

* docker image 확인 명령 : docker images   or  docker image ls 
    -q 옵션: docker image의 id만 확인 가능. -> 다른 명령어와 함께 자주 쓰인다.

docker pull
1. docker pull [이미지 이름] : docker image 다운로드
    ex) docker pull ubuntu : ubuntu 최신버전 설치된다. -> docker pull ubuntu:20.04 하면 20.04버전 다운로드된다.


docker rmi 삭제할이미지이름 : 도커 이미지 삭제 명령
 1. docker rmi 이미지이름[:태그] or ImageID

docker rm 삭제할컨테이너이름 : 도커 컨테이너 삭제

docker create : 컨테이너 생성 명령어. return으로 컨테이너의 id를 출력한다.
 1. --name 옵션 사용 : docker create --name 내가원하는컨테이너이름 이미지이름
   ex) docker create --name cwj ubuntu : cwj이름으로 ubuntu 이미지에대한 컨테이너 생성.

docker ps : 현재 실행 중인 컨테이너 확인 (모든 컨테이너를 확인하려면 -a 옵션 사용)



