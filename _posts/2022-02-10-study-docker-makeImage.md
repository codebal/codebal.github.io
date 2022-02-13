---
title : "docker make image"
---

- commit 명령어
    - 실행된 컨테이너를 이미지로 만든다
    - hub 이미지를 받아서 컨테이너를 만들고 추가작업후에 새로운 이미지 생성
    - docker commit {container id or name} {new image name}
    - ex) docker commit 65d60d3dd306 ubuntu:custom

- DockerFile 파일로 이미지 만들기
    - DockerFile 을 만든다
        - vi DockerFile
        - FROM {docker image name}
        - RUN {command}
        - ex)
            ```
            FROM ubuntu:bionic
            RUN apt-get update
            RUN apt-get install -y git
            ```
    - build
        - docker build -t ubuntu:git-added

- 허브 레포지토리 이용
    - https://hub.docker.com/ 가입
    - public repository 를 하나 생성
    - 로컬 command 창에서 로그인
        ```
            docker login
        ```
        - 아이디, 패스워드 입력
    - 이미지에 새로운 태그 생성
        ```
            docker tag ubuntu:latest {hub id}/{repository name}:{tag}
        ```
    - 새로운 태그로 만들어진 이미지 확인
        ```
            docker images
        ```
    - repository에 이미지를 push
        ```
            docker push {image name}:{tag}
        ```
    - https://hub.docker.com/ repositories에서 push된 이미지 확인