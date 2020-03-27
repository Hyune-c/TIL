# Heroku

웹 애플리케이션 배치 모델로 사용되는 여러 프로그래밍 언어를 지원하는 클라우드 PaaS 입니다.

아래는 `https://github.com/codesquad-memeber-2020/signup-5.git` 의 `dev` branch 를 Heroku 의 `signup-5-dev` 의 `master` branch 올리고 기동하는 스크립트입니다.

## Setting

- `dev` branch local 로 받기

```shell script
> git clone -b dev --single-branch https://github.com/codesquad-memeber-2020/signup-5.git signup-5-dev
> cd signup-5-dev
```

- install CLI

```shell script
> brew tap heroku/brew && brew install heroku
```

- login

키를 받거나

```shell script
> heroku authorizations:create
Creating OAuth Authorization... done
Client:      <none>
ID:          *********-a0d1-446c-a714-*********
Description: Long-lived user authorization
Scope:       global
Token:       *********-cbd8-4453-a445-*********
Updated at:  Wed Mar 25 2020 02:43:18 GMT+0900 (GMT+09:00) (less than a minute ago)
```

Browser 를 통해 로그인 합니다.

```shell script
> heroku login
```

- create Heroku App

```shell script
> heroku create signup-5-dev
> heroku apps:destroy signup-5-dev
```

- remote setting

```shell script
> heroku git:remote -a signup-5-dev
> git remote -v
heroku	https://git.heroku.com/signup-5-dev.git (fetch)
heroku	https://git.heroku.com/signup-5-dev.git (push)
origin	https://github.com/codesquad-memeber-2020/signup-5.git (fetch)
origin	https://github.com/codesquad-memeber-2020/signup-5.git (push)
```

- deploy

```shell script
> git subtree push --prefix BE/signup/ heroku master
git push using:  heroku master
Enumerating objects: 333, done.
Counting objects: 100% (333/333), done.
Delta compression using up to 8 threads
Compressing objects: 100% (144/144), done.
Writing objects: 100% (333/333), 89.93 KiB | 17.99 MiB/s, done.
Total 333 (delta 96), reused 300 (delta 94)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Gradle app detected
remote: -----> Spring Boot detected
remote: -----> Installing JDK 1.8... done
remote: -----> Building Gradle app...
remote: -----> executing ./gradlew build -x test
remote:        Downloading https://services.gradle.org/distributions/gradle-6.2.2-all.zip
remote:        .............10%.............20%.............30%..............40%.............50%.............60%.............70%..............80%.............90%.............100%
remote:        To honour the JVM settings for this build a new JVM will be forked. Please consider using the daemon: https://docs.gradle.org/6.2.2/userguide/gradle_daemon.html.
remote:        Daemon will be stopped at the end of the build stopping after processing
remote:        > Task :compileJava
remote:        > Task :processResources
remote:        > Task :classes
remote:        > Task :bootJar
remote:        > Task :jar SKIPPED
remote:        > Task :assemble
remote:        > Task :check
remote:        > Task :build
remote:
remote:        BUILD SUCCESSFUL in 43s
remote:        3 actionable tasks: 3 executed
remote: -----> Discovering process types
remote:        Procfile declares types     -> (none)
remote:        Default types for buildpack -> web
remote:
remote: -----> Compressing...
remote:        Done: 71.5M
remote: -----> Launching...
remote:        Released v3
remote:        https://signup-5-dev.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/signup-5-dev.git
 * [new branch]      3f6084865c0da460bec19a2e4e69ebd5cf8937b3 -> master
```

- ssh 로 Heroku App 접속

```shell script
> heroku ps:exec -a signup-5-dev
```

- Tip
  - Server time Setting

    ```shell script
    > heroku config:set TZ=Asia/Seoul
    ```

- 요약

> 아래 스크립트 실행시 local 의 소스가 올라갑니다.

```shell script
> rm -rf signup-5-dev

> git clone -b dev --single-branch https://github.com/codesquad-memeber-2020/signup-5.git signup-5-dev

> cd signup-5-dev

> heroku apps:destroy signup-5-dev
# signup-5-dev 입력

> heroku create signup-5-dev
> heroku config:set TZ=Asia/Seoul

> heroku git:remote -a signup-5-dev

> git subtree push --prefix BE/signup/ heroku master
```

## 참고 자료

<https://www.a-mean-blog.com/ko/blog/%EB%8B%A8%ED%8E%B8%EA%B0%95%EC%A2%8C/_/Heroku-%ED%97%A4%EB%A1%9C%EC%BF%A0-%EA%B0%80%EC%9E%85-Heroku-CLI-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-%EA%B0%84%EB%8B%A8-%EC%82%AC%EC%9A%A9%EB%B2%95>