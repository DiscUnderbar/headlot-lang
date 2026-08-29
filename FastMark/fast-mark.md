# fast mark

fastmark 는 수정을 더 쉽게 하기 위한 md 문서가 낡은걸 해결하기 위한 프로그래밍 언어다.

## 이게 무엇이냐

fastmark 는 수정을 쫌더 쉽게 해주다.

일반 markdown:

```markdown
# Tennin programming language

Tennin programming language is ...
```

하지만 fastmark 는

```fastmark
# ({name}) programming language

({name}) programming language is ...
```

이런식이다.

그리고 밖에서 variable name = "Tennin"; 이런식으로 파싱 하면

```markdown
# Tennin programming language

Tennin programming language is ...
```

이 된다. 참고로 여기서 `({` 라고 쓰기 위해선 &amp;lf; (left format) 그리고 `})` 는 &amp;rf; (right format) 이라고 하면 된다.

또한 줄넘김이 있으면 자동으로 \ 를 삽입한다. markdown 에선 문제가 줄넘김이 있어도 그게 preview 에선 그게 진짜 줄이 넘겨 진걸론 안보이고 \ 를 추가 해야지 보이는게 문제였는데 이 fastmark 에선 \ 를 추가 안해도 자동으로 \ 를 삽입해준다. 또한 띄어 쓰기도 markdown 에선 그게 언제나 띄어쓰기 하나로 보이고 ``` ``` 안에 있어야만 그게 뜨어쓰기가 반영이 되는데 fastmark 에선 띄어쓰기가 여러개 있어도 그 뜨어쓰기가 하나만 있을땐 ` ` 로 보이는데 여러개 있을땐 `&nbsp;&nbsp;` 이런식으로 변환 된다.

## 챕터

이 글의 챕터다. Fast Mark 에선 글이 그냥 계속 쭉 내려가는 그런 글이 아니다. tree 형태다.

```
({name}) programming language  (Tennin programming language is a ...)
├─ killer use case             (killer use case is ...)
├─ 문법                         (문법 ...)
|  ├─ 인자 함수                 (인자함수는 ...)
|  └─ Expand                   (Expand 는 ...)
|  (지금까지 문법이였습니다. 그 다음 ...)
├─ 실행 모델                    (실행 모델은 간단히 ...)
├─ 표준 라이브러리               (표준 라이브러리는 ...)
└─ 역사                        (이 언어는 처음에 ...)
```

이런식이다. 그리고 여기서 저거 killer use case, 문법, 인자함수, Expand 저게 다 챕터다.

또한 챕터엔은 그 안에 또 챕터가 있을 수도 있고 처음에 시작하는 챕터도 있고 이 아래 자식 챕터에서 문법에서 인자함수, Expand 사이에도 내용을 넣을수도 있고 문법 바로 앞 인자 함수 위, 문법 아래 거기에도 너을수가 있고 끝에도 더 내용을 넣을수도 있다.

기본적으로 챕터는 fastmark 에서 이렇게 쓴다.

```fastmark
@chap 챕터 이름 {
    챕터 내용
    @chap 챕터 이름 {
        챕터 내용
    }
    @chap 챕터 이름 {
        챕터 내용
    }
}
```

(참고로 `@` 는 fastmark 에서 쓸려면 `@\` 라고 써야 한다. 그리고 `@\` 이라고 쓸려면 `@\\` 이라고 써야 하고 ...)

이러면 이제 나중에 이런식으로 쓰면 좋은게 글의 구조가 명확하게 보인다. 그리고 수정 하는것도 챕터의 경로를 입력해서 (챕터 이름/챕터 이름 이런식으로 입력하면 찾기 가능) 쉽게 챕터를 찾을수 있다. 그리고 이 챕터에 몇번째줄 이런것도 이 프레임워크 함수로 내장 되어 있다. 그래서 이 프레임워크 함수로 쉽게 이 챕터 내용이나 이 챕터에 특정 줄을 쉽게 코드로 찾고, 수정할수 있다.

예시:

```fastmark
@chap ({name}) 프로그래밍 언어 {
    ({name}) 프로그래밍 언어
    @chap 문법 {
        문법이다.
        @chap 인자 함수 {
            인자 함수는 ...
        }
        @chap 함수 선언 {
            함수 선언은 ...
        }
    }
}
```

또한 @chap 과 그 챕터 이름이 구분이 잘 않된다면 `@chap | 챕터 이름` 이렇게 적는게 가능하다.

예시:

```fastmark
@chap | ({name}) 프로그래밍 언어 {
    ({name}) 프로그래밍 언어
    @chap | 문법 {
        문법이다.
        @chap | 인자 함수 {
            인자 함수는 ...
        }
        @chap | 함수 선언 {
            함수 선언은 ...
        }
    }
}
```

이런식으로 하는것도 가능하다.

## 변수 보간

변수 보간이 가능하다. 위에 예시 기능으로 먼저 나왔 었는데 ({변수 이름, 태그1, 태그2}) 이런식으로 작성한다.

먼저 기본 문법은 ({등록된 변수}) 다. 그리고 여기서 만약 등록된 변수의 네이밍 컨벤션을 PascalCase 로 하고싶다. 이때 태그를 사용한다. 또한 태그의 기본값 설정도 가능하다.

```fastmark
#default tag name "PascalCase";

@chap | ({name}) 프로그래밍 언어 {
    ({name, "camelCase"}) 언어.
}
```

이렇게 하는거다.

그래서 또 태그를 어디에 쓰냐면 뭐 특정 이건 조사 태그 붙여서 "josa 가", "josa 나" 이런식으로 태그를 붙칠수도 있다.

그리고 만약 태그를 쫌 많이 달아야 할때. 조사처럼 그때는 이런게 가능하다.

```fastmark
#default tag name "PascalCase", "josa 가";
```

이런게 아니라

```fastmark
#default tag name "PascalCase", callback (script, index, variable) => {
    #include <string>

    std::string callback {
        if (variable[variable.lenght() - 1]) {
            ... 어쨋든 조사 구해서 조사 태그 반환하는 함수
        }
    }
};
```

이런식으로 이제 callback (script, index, variable) => { C++ 코드 } 로 쫌 복잡하게 하고 싶을때 이렇게 할수 있다. 그런데 이건 너무 복잡하니까 그냥 이 name 을 봐꿀때 마다 그냥 josa 도 봐꾸는게 좋다. 직접 코드 짜기 귀찮으니까.
