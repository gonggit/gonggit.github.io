---
layout  : wiki
title   : EnumType.String 컬럼 Enum property로 정렬하기 
summary :  
date    : 2023-02-15 16:56:22 +0900
updated : 2023-02-15 20:51:49 +0900
tag     : springboot jpa mysql 
resource: AB/0651B1-874E-48B8-A344-34F61A2CAEC5
toc     : true
public  : true
parent  : [[/spring-boot]] 
latex   : false
---
* TOC
{:toc}

# 흔한 구조 
누구나, 어디에나 있는 흔한 엔티티가 있다고 가정하자.
```kotlin
@Entity
@Table(name = "has_enum_entity")
data class HasEnumEntity(
    @Enumerated(value = EnumType.String)
    val career: CareerStep,
)

// 순서를 나타내는 Enum.
enum class CareerStep(val value: Int) {
    NOVICE(0), ADVANCED_BEGINNER(1), COMPETENT(2), PROFICIENT(3), EXPERT(4);
}
```

그리고 해당 Entity와 대응되는 테이블은 다음과 같다.
```sql
create table if not exists has_enum_entity(
  no bigint auto_increment primary key,
  career varchar(100) null
)
```

그리고 대략 아래와 같은 데이터가 저장되어있다.
```
no,career
1, NOVICE 
2, ADVANCED_BEGINNER 
3, COMPETENT 
4, EXPERT 
5, PROFICIENT 
```

## 그러던 어느 날
해당 테이블을 사용하는 팀에서 아래와 같은 요구사항을 전달해왔다.
> `career` 컬럼의 value property를 기준으로 정렬하고 싶어요!

## 머리를 싸맨다.
어떻게 할 것인가? 어찌보면 당연한 요구사항이다. CareerStep Enum은 순서가 정해진 Enum이며, 때문에 정렬시 의도 한순서대로 `NOVICE -> ADVANCED_BEGINNER -> COMPETENT -> EXPERT -> PROFICIENT` 표현되어야 한다. 
하지만 has_enum_entity 테이블에 `ORDER BY career` 을 한다면, 알파벳 사전 순인 `ADVANCED_BEGINNER -> COMPETENT -> EXPERT -> NOVICE -> PROFICIENT` 순서로 정렬되어 나올 것이다. 과연 이 문제를 어떻게 해결해야 할까? 

역시나 구글에 검색해 보니(`spring boot order by value of enum`) 이미 누군가 했던 고민인것 같다.
아래는 선정된 답변에서 제안한 해결 방법들이다.

### 방법 1
- **EnumType.String** 대신 **EnumType.Ordinal**을 사용하라. 

이게 될려면 테이블에 저장된 career 컬럼의 타입(varchar -> int) 뿐만아니라 값을 모두 원하는 Ordinal 타입으로 변경해야 한다. 또한 Ordinal 값과 정렬하기 원하는 대상 필드값이 다를 수도 있다. 그리고 애초에 기본값인 Ordinal이 아닌 String으로 저장한 이유가 있을텐데, 막상 적용하려니 손이 가지 않았다. 

### 방법 2
- enum을 Entity로 변경하고 정렬하기 원하는 기준값을 추가로 저장하라.

아마도 Enum을 포함하는 @Embeddable 클래스로 변경한 후 @Embedded 시키라는 의미가 아닐까 싶다. 테이블에 새로운 컬럼, 이를테면 career_value 등의 컬럼을 추가한 후 정렬하기 원하는 값을 저장하도록 한 후, career와 career_value를 멤버 필드로 갖는 CareerEntity 클래스를 @Embeddable로 선언 하라는 것 같다.

꽤 나쁘지 않은 방법이라고 생각했다. 정렬 대상값을 임의대로 변경할 수도 있고 원래 String 값까지 보존하지 괜찮아 보였다. 다만 테이블을 보았을 때 의미불명의 컬럼이 존재하는 것이 조금 마음에 들지 않아보였다. 만약 테이블 크기가 충분히 커진다면 이 방법을 사용해야 할 것 같다.

### 방법 3
- @Format annotation을 사용하라.

답변자는 성능상 이슈로 가장 마지막 방법이라고 제안했지만, 나는 그래도 가장 마음에 들었다. 성능상 문제가 될 구간까지는 10년 넘게 걸릴 것 같았기 때문이었다. 테이블에 새로운 컬럼을 추가 할 필요도 없고, 코드에서 정렬 기준을 관리할 수 있으니 꽤 좋은 방법같았다.
@Format 애노테이션은 이렇게 정의되어있다.

>Defines a formula (derived value) which is a SQL fragment that acts as a @Column alternative in most cases.
Represents read-only state.

>In certain cases @ColumnTransformer might be a better option, especially as it leaves open the option of still
being writable.

그러니까 SQL 구문의 일부로서 @Column으로 정의된 필드를 대체하는 방식으로 작동한다는 것이다. 예를 들어 @Formula annotation이 정의된 필드는 실제 SQL로 변환시 @Forumla에 정의된 SQL 구문으로 치환된다.

결국 내가 작성한 HasEnumEntity의 최종 버전은 아래와 같았다.

```kotlin
@Entity
@Table(name = "has_enum_entity")
data class HasEnumEntity(
    @Enumerated(value = EnumType.String)
    val career: CareerStep,
) {
    @Formula(value = """
            CASE career
            WHEN 'NOVICE' THEN 0 
            WHEN 'ADVANCED_BEGINNER' THEN 1 
            WHEN 'COMPETENT' THEN 2 
            WHEN 'EXPERT' THEN 3 
            WHEN 'PROFICIENT' THEN 4 
            ELSE 5 
            END
    """)
    private val careerValue: Int = 0
}
```

이렇게 클래스를 작성해두고 careerValue를 기준으로 정렬하면 ex) findAllByOrderByCareerValue() order by 구문에 career_value 대신 Formula에 선언한 구문으로 치환된다.

이 떄 Hibernate 로그를 보면 대략 이런식으로 생성된다.

```sql
select distinct has0_.`no` as no1_277_,
         CASE has0_.career
             WHEN 'NOVICE' THEN 0
             WHEN 'ADVANCED_BEGINNER' THEN 1
             WHEN 'COMPETENT' THEN 2
             WHEN 'EXPERT' THEN 3
             WHEN 'PROFICIENT' THEN 4
             ELSE 5 
             END
                           as formula1_
from has_enum_entity has0_
order by
         CASE has0_.career
             WHEN 'NOVICE' THEN 0
             WHEN 'ADVANCED_BEGINNER' THEN 1
             WHEN 'COMPETENT' THEN 2
             WHEN 'EXPERT' THEN 3
             WHEN 'PROFICIENT' THEN 4
             ELSE 5 
             END
        asc
limit 10
```

(위에 애써 alias 선언해놓고 order by 구문에서 다시 CASE 문을 타는 이유는 잘 모르겠다.)

### 그 외
몇 가지 생각해볼 수 있는 방법이 있을 것이다. `CareerStep`의 메타데이터를 저장하는 별도 테이블을 생성한 후, HasEnumEntity를 가져오는 과정에서 career 필드로 조인한 후 정렬할 수도 있을 것이고, Native query를 사용할 수도 있을 것이다. 만약 Pagination을 할 필요가 없다면 모든 데이터를 서버에 가져온 후 정렬하는 방식도 가능할 것이다.

다만 현실에서는 몇 가지 제약사항이 있었기 때문에 세번째 방법을 적용했다. 데이터의 양이 많아질수록 성능이 저하될 것은 불보듯 뻔하지만 그 때의 튜닝은 그 때의 누군가에게 맡기도록 한다.

*코드는 모두 임의 작성하였으므로 컴파일 되지 않을 수도 있다(...)*

## 참고
[StackOverflow](https://stackoverflow.com/questions/3605655/control-sort-order-of-hibernate-enumtype-string-properties)
