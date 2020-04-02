# Process

## ForeGround vs BackGround

`job` 명령어를 통해 ForeGround 와 BackGround 간의 작업 전환이 가능합니다

### ForeGround (이하 fg)

- 명령의 처리가 끝날 때까지 대기합니다
  - 프롬프트가 출력되지 않습니다
- 한 터미널에서 하나의 프로세스만 실행 가능합니다

### BackGround (이하 bg)

- 명령의 마지막에 `&` 를 넣어 실행합니다
- 명령의 처리가 끝날 때까지 대기하지 않습니다
  - 프롬프트가 출력되어 다른 명령이 가능합니다
- 한 터미널에서 여러 개의 프로세스를 동시에 실행 가능합니다
  - stdout 을 공유함으로 명령의 처리가 같은 터미널에 보입니다
- 명령의 처리 시간이 긴 작업을 할 때 용이합니다

## & vs disown vs nohup

> SIGHUP : 사용자 터미널의 단절시 발생하는 signal 입니다

### &

- 프로세스를 bg 에서 실행합니다
- 프로세스로의 stdin 을 막습니다

### disown

- 프로세스를 job control에서 제외합니다
  - 터미널 종료시 SIGHUP을 보내지 않습니다
  - stdout 은 연결되어있습니다

### nohup

- 터미널과 프로세스의 연결을 끊습니다
  - 터미널 종료시 SIGHUP을 보내지 않습니다
  - stdout 을 nohup.out으로 리다이렉팅합니다
  - stdout 의 연결도 끊어집니다

## 터미널과 독립적인 프로세스를 만드는 방법

ForeGound 의 작업을 동작시킨 터미널이 단절되면 SIGHUP 이 발생하여 해당 프로세스를 종료 시킵니다.  
따라서 터미널이 종료된 후에도 프로세스의 작동을 위해서는 `nohup` 와 `&` 를 모두 사용하면 됩니다.

```shell script
ex) nohup ./gradlew bootRun &
```

## 참고자료

<https://velog.io/@jakeseo_me/nohup-disown-%EB%8A%94-%EC%96%B8%EC%A0%9C-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8D%A8%EC%95%BC%EB%90%A0%EA%B9%8C-9fjv7q9bz8>
