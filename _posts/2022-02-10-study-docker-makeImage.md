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