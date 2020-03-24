# Heroku

웹 애플리케이션 배치 모델로 사용되는 여러 프로그래밍 언어를 지원하는 클라우드 PaaS 입니다.

## Setting

- install CLI

```shell script
brew tap heroku/brew && brew install heroku
```

- login

```shell script
heroku login
```

- create repository

```shell script
# gradle buildpack 을 가져옵니다.
 heroku create signup-5-test --buildpack https://github.com/heroku/heroku-buildpack-gradle.git
Creating ⬢ signup-5-test... done
Setting buildpack to https://github.com/heroku/heroku-buildpack-gradle.git... done
https://signup-5-test.herokuapp.com/ | https://git.heroku.com/signup-5-test.git
```

- remote setting

```shell script
 heroku git:remote -a signup-5-test
set git remote heroku to https://git.heroku.com/signup-5-test.git
 choibyunghyeon  ~/Documents/github/codesquad/signup-5/BE/signup   server/feature/user-join >R>
 git remote -v
heroku	https://git.heroku.com/signup-5-test.git (fetch)
heroku	https://git.heroku.com/signup-5-test.git (push)
origin	https://github.com/codesquad-memeber-2020/signup-5.git (fetch)
origin	https://github.com/codesquad-memeber-2020/signup-5.git (push)
```

- push

> Error 발생!!!!!!!!

```shell script
 git push heroku server/feature/user-join:master
Enumerating objects: 146, done.
Counting objects: 100% (146/146), done.
Delta compression using up to 8 threads
Compressing objects: 100% (105/105), done.
Writing objects: 100% (146/146), 89.86 KiB | 7.49 MiB/s, done.
Total 146 (delta 25), reused 49 (delta 3)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> App not compatible with buildpack: https://github.com/heroku/heroku-buildpack-gradle.git
remote:        Could not find a 'gradlew' script or a 'build.gradle' file! Please check that they exist and are commited to Git.
remote:
remote:        More info: https://devcenter.heroku.com/articles/buildpacks#detection-failure
remote:
remote:  !     Push failed
remote: Verifying deploy...
remote:
remote: !	Push rejected to signup-5-test.
remote:
To https://git.heroku.com/signup-5-test.git
 ! [remote rejected] server/feature/user-join -> master (pre-receive hook declined)
error: failed to push some refs to 'https://git.heroku.com/signup-5-test.git'
```

> gradlew, build.gradle 이 해당 경로에 있음은 확인 됨

```shell script
 choibyunghyeon  ~/Documents/github/codesquad/signup-5/BE/signup   server/feature/user-join >R>
 ls -lrt
total 40
drwxr-xr-x  3 choibyunghyeon  staff    96  3 23 15:30 gradle
-rwxr-xr-x  1 choibyunghyeon  staff  5764  3 23 15:30 gradlew
-rw-r--r--  1 choibyunghyeon  staff  2942  3 23 15:30 gradlew.bat
-rw-r--r--  1 choibyunghyeon  staff    28  3 23 15:30 settings.gradle
drwxr-xr-x  4 choibyunghyeon  staff   128  3 23 15:30 src
drwxr-xr-x  8 choibyunghyeon  staff   256  3 23 15:36 build
-rw-r--r--  1 choibyunghyeon  staff   901  3 23 15:46 build.gradle
drwxr-xr-x  4 choibyunghyeon  staff   128  3 24 03:25 logs
```

## 참고 자료

<https://www.a-mean-blog.com/ko/blog/%EB%8B%A8%ED%8E%B8%EA%B0%95%EC%A2%8C/_/Heroku-%ED%97%A4%EB%A1%9C%EC%BF%A0-%EA%B0%80%EC%9E%85-Heroku-CLI-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-%EA%B0%84%EB%8B%A8-%EC%82%AC%EC%9A%A9%EB%B2%95>
