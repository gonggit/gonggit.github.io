---
layout  : wiki
title   : grep은 개발자의 좋은 친구 
summary : 찾고싶은 것이 있다면 찾아보세요 
date    : 2025-03-25 00:05:11 +0900
updated : 2025-03-25 00:16:42 +0900
tag     : grep, cli 
resource: BD/C03CAB-6428-439C-BC15-AC37E99291BF
toc     : true
public  : true
parent  : 
latex   : false
---
* TOC
{:toc}

# grep
여러분이 개발자라면, 한 번이라도 터미널을 사용해 보았다면 한 번쯤은 반드시 사용해 보았을 명령어다. 주로 파일(텍스트)에서 특정 패턴을 검색하는 데 유용하다. 로그 분석, 설정 파일 검색, 소스 코드 내 특정 문자열 찾기 등에 활용할 수 있다.

만약 cli에 익숙하다면, 혹은 적절한 GUI를 사용할 수 없는 환경이라면(현대의 에디터에서 Cmd + F 와 같은 찾기 명령어) grep은 여러분이 하고자하는 거의 모든 것을 할 수 있는 유용한 도구가 될 것이다.


---

### 1. 특정 문자열 포함된 행 찾기
```sh
# 로그 파일에서 "error"가 포함된 행을 찾는다.
grep --text "error" application.log  # -a
```

---

### 2. 대소문자 구분 없이 검색
```sh
# Ignore case, 그러니까 대소문자 구분 없이 "Warning", "WARNING", "warning" 등을 모두 검색할 때 사용한다.
grep --ignore-case "warning" application.log # -i
```

---

### 3. 특정 단어만 검색
```sh
# "failed"나 "failing"은 제외하고 "fail"이라는 단어만 검색한다.
grep --word-regexp "fail" application.log  # -w
```

---

### 4. 검색 결과에서 특정 단어 제외
```sh
# "error"가 포함된 행 중 "timeout"이 없는 행만 출력한다.
grep --text "error" application.log | grep --invert-match "timeout"  # -v
```

---

### 5. 줄 번호 함께 출력
```sh
# 소스 코드에서 "TODO"가 있는 줄 번호를 함께 출력한다.
grep --line-number "TODO" source_code.java  # -n
```

---

### 6. 검색 결과 앞뒤 줄도 함께 출력
```sh
# "Exception"이 포함된 행을 기준으로 앞 2줄, 뒤 3줄까지 함께 출력한다.
grep --text "Exception" application.log --before-context=2 --after-context=3  # -B 2 -A 3
```

---

### 7. 특정 파일 확장자에서 검색
```sh
# src/ 디렉터리에서 .java 파일만 대상으로 "import"가 포함된 행을 검색한다.
grep --text "import" --recursive --include="*.java" src/
```

---

### 8. 특정 파일 제외하고 검색
```sh
# config/ 디렉터리에서 "password"가 포함된 행을 검색하되, .log 파일은 제외한다.
grep --text "password" --recursive --exclude="*.log" config/

# 자매품. 특정 디렉토리를 제외하고 검색한다
grep --text "error" --recursive --exclude-dir="logs" src/
```
---

### 9. 하위 디렉터리 포함하여 검색
```sh
# project/ 디렉터리 내부의 모든 파일에서 "TODO"를 검색한다.
grep --text "TODO" --recursive project/  # -a -r
```

### 10. 검색 결과에서 파일 이름만 출력
```sh
# src/ 디렉터리에서 "FIXME"가 포함된 파일 이름만 출력한다.
grep --text "FIXME" --recursive --files-with-matches src/  # -a -r -l
```

---

이처럼 `grep`을 활용하면 텍스트 검색 작업을 효과적으로 수행할 수 있다. `descriptive option`을 사용하면 명령어의 가독성이 높아지고, `short option`은 입력을 줄이는 데 유용하다. 😃
