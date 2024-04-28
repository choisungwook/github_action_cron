# 개요
* github action cron테스트
* 자세한 내용은 [블로그](https://malwareanalysis.tistory.com/725)를 참고

# act로 로컬에서 실행하는 방법

1. docker.sock 설정

```sh
# 1. docker.sock 위치 확인
$ docker context ls

# 2. 만약 docker.sock위치가 /var/run/docker.sock가 아니라면 symbolic링크 설정

sudo ln -s ~/.docker/run/docker.sock /var/run/docker.sock
```

2. act가 사용하는 DOCKER_HOST설정

```sh
export DOCKER_HOST=$(docker context inspect --format '{{.Endpoints.docker.Host}}')
```

3. act 실행
* --container-daemon-sockets는 컨테이너 마운트할 때 docker.sock 위치


```sh
act  --container-daemon-socket /var/run/docker.sock -W ./.github/workflows/docker_build.yml
```

# 참고자료
* https://github.com/nektos/act/issues/1051
* https://www.freecodecamp.org/news/how-to-run-github-actions-locally
