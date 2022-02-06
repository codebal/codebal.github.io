---
title : "study docker basic"
---

- docker 정보
    - docker info

- hub에서 docker image 검색
    - docker seach {name}

- bun에서 image pull
    - docker pull {image name}

- 저장된 docker image 확인
    - docker images
    - 맥 image 저장 위치 : ~/Library/Containers/com.docker.docker/Data/vms/0/

- 저장된 image 제거
    - docker rmi {image name}

- 컨테이너 정보
    - docker ps
    - docker ps -a // all

- 컨테이너 정지
    - docker stop {name or id}

- image로 컨테이너 생성하고 실행
    - docker run {image name}
    - docker run -d {image name} // background
    - docker run --name {name} {image name} // run with container name
    - docker run -p {host port}:{container port} {image name} // publish container port
        - ex) docker run --name ws -p 8080:80 httpd 
        > httpd 이미지사용, 컨테이너 이름은 ws, 호스트의 8080포트로 컨테이너 80포트를 퍼블리시
    - docker run -v {host directory}:{container directory}
        > - 컨테이너의 디렉토리를 호스트의 디렉토리에 마운트
        > - ex) docker run --name ws -p 8080:80 -v ~/test:/user/local/test httpd
        >   - 호스트의 ~/test 디렉토리는 컨터이너의 /user/local/test 의 디렉토리 역할을 하게 됨

- 컨테이너 정지
    - docker stop {name or id}
    - docker stop $(docker ps -q) // stop all runnung containers

- 컨테이너 시작
    - docker start {name or id}
    - docker start -d {name or id} // background

- 컨테이너 로그 보기
    - docker logs {name or id}
    - docker logs -f {name or id} // continuous

- 컨테이너 삭제
    - docker rm {name or id}
    - docker rm --force {name of id} // force remove
    - docker rm $(docker ps -a -q) // remove all stop containers

- 컨테이너에 명령어 실행
    - docker exec {name or id} {command}
        - ex) docker exec ws1 pwd
        - ex) docker exec -it ws1 /bin/sh; exit;
        > - ws1 컨테이너에 접속하여 쉘실행. exit 명령 입력하여 종료할때까지 유지됨. 종료후에 exit로 터미널 종료
        > - /bin/sh 대신 /bin/bash 가능

