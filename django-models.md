##Models정리

1. Person 클래스로 DB테이블 만듦

```from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```
    
 - 만들면  아래 와 같은 테이블 생성이된다 이때 지정하지 않아도
기본키는 id로 잡히는것으로 보인다

```CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL
);
```

 - 테이블이 지정되면 재정의할수있다.
 - id로 기본키 자동으로 생성된다.
 - 장고에 지정된 sql로 사용하여 sql문으로 생성된다.


 2. models가 포함된 폴더를 settings파일안에 installed_app 에 표기를 해주여한다.

 3. 필드
  - 필드타입 : 데이타베이스 저장될때와 html로 표현될때 조금다르다
  - 내장함수를 통하여 유저는 쉽게 업무를 할수있게 해준다.
  - null : null이 true이면 널값을 넣어준다. 기본은 false이다
  - blank : 빈칸을 만들어주는것이며 기본은 false이다.
  - 테이블을 만들고 makemigrations을 하고 migrate를 실행하여 테이블을 업데이트를 시켜준다
  - 테이블을 만들때 미리 필드에 입력될 값을 미리 지정해서 입력받은 값의 데이타를 저장할수있는것으로 보임
  - ./manage shell사용시 반드시 form(생성app안의 models) import (불러올 테이블명을 적어주면됨)
  
  - 기본키를 지정할수도있다
  - primary_key = True를 사용
  - 사용후에 값을 변경하게되면 자동으로 키를 복사하여 생성한다
  - 중복이상으로 보임
  
  - unique : 값이 ture이면 테이블은 고유해야된다

4. verbose filed
 - verbose란 models에서 테이블 생성할 때 각필드의 명칭을 지정해줄수있다.
 - 명칭을 지정하는데 foreignkey,manytomanyfiled , onetoonefiled에는 명칭을 쓸때 verbose_name을 사용하여 지정할수있다.
 - 만약 사용하지 않는다면 변수에서 _을 뺀나머지로 지정된다
5. 관계이해 - 좀 이해하기 힘든 코드이다.....
 - 다대일 관계
 	- 외래키로 불러와서 쓰는거처럼보임
 	- django.db.models.ForeignKey()를 불러와 사용
 - 다대다 관계
 	- ManToManyFiled() 
 	- 중간모델 through ...
	 	- 사용할때 조건이 있다.

 - 일대일 관계
 	- OneToOneField사용
 	- 변수이름에 파이썬의 예약어 pass같은것을 사용할수없다
 	- 변수이름에 __ 두개를 사용할수없다.
6. 메타데이타
 - 모델단위의 옵션?
7. 모델 속성
 - 모델의 인스턴스에서만 접근해서 사용할수있다.

8. 모델 상속
 - 기본적인 상속은 파이썬을 따름
 - 1. 부모클래스는 실제로 테이블을 만들지안하고 자식클래스에서 테이블을 만드는 방법
 	- 클래스안에 meta클래스를 추가하여 abstract=True로 하면 추상 클래스가 만들어진다
 - 2. 다른 app에서 선언되어 사용중인 모델을 상속하는 경우 부모 자식 서로 별개의 구조를 가지며 독맂벅으로 사용한다
 - 3. 파이선 코드 레벨 만 수정할때 proxy모델을 사용
 - 다중상속....하나도 모르겠음