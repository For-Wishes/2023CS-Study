# 💡 MVC 패턴이란 무엇인가?

# ✅ MVC 패턴이란?
## MVC 패턴이란?
MVC란 Model-View-Controller의 약자로 애플리케이션을 세 가지 역할로 구분한 개발 방법론이다.  
아래의 그림처럼 사용자가 Controller를 조작하면 Controller는 Model을 통해 데이터를 가져오고 그 데이터를 바탕으로 View를 통해 시각적 표현을 제어하여 사용자에게 전달하게 된다.  
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDpdks%2FbtrjV9EuRJ3%2FegwkkBELr5i0oYOv4t9Qy1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDpdks%2FbtrjV9EuRJ3%2FegwkkBELr5i0oYOv4t9Qy1%2Fimg.png)

<br/>

이러한 패턴을 성공적으로 사용하면, 사용자 인터페이스로부터 비즈니스 로직을 분리하여 애플리케이션의 시각적 요소나 그 이면에서 실행되는 비즈니스 로직을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있게 된다.

<br/>

### 위의 개념을 WEB에 적용한다면
- 사용자가 웹사이트에 접속 (Users)
- Controller는 사용자가 요청한 웹페이지를 서비스하기 위해서 모델을 호출 (Manipulates)
- Model은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후 그 결과를 Return
Controller는 Model이 리턴한 결과를 View에 반영 (Updates)
- 데이터가 반영된 View는 사용자에게 보여짐 (Sees)

<br/>

### MVC 패턴은 디자인 패턴? 아키텍처 패턴?
> MVC 패턴을 디자인 패턴이라고 하는 경우도 있고 아키텍처 패턴이라고 하는 경우도 있어서 둘의 차이를 알아보았다.
> 

<br/>

- 디자인 패턴    
    : 소프트웨어 디자인에서 공통적으로 발생하는 문제에 대해 재사용 가능한 해결책을 말한다. 상황에 맞게 사용될 수 있는 문제들을 해결하는데에 쓰이는 템플릿을 의미한다. 프로그래머가 어플리케이션이나 시스템을 디자인할 때 공통된 문제들을 해결하는데에 쓰이는 형식화 된 가장 좋은 패턴이다.    
- 아키텍처 패턴    
    : 아키텍처 패턴은 디자인 패턴과 유사하지만 범위가 더 넓다. 아키텍처 패턴은 소프트웨어 공학의 다양한 문제를 해결하는데, 예를 들어 컴퓨터 하드웨어 성능 제한, 비즈니스 위험의 최소화와 고가용성 등이 있다. 일부 아키텍처 패턴은 SW 프레임워크 안에 구현되어 있다. 아키텍처 패턴이 시스템의 이미지를 전달하기는 하지만 아키텍처 자체를 의미하는 것은 아니다. 다양한 아키텍처가 동일한 패턴을 구현하고 관련 특성을 공유할 수 있다.
    
<br/>

간단하게 정리하자면 디자인 패턴과 아키텍처 패턴은 소프트웨어공학에서 발생하는 문제를 해결한다는 점에서 비슷하지만, 디자인 패턴은 특정 문제를 해결하기 위한 방법이고, 아키텍처 패턴은 전체적인 소프트웨어에서 발생하는 문제들을 해결하기 위한 방법이라고 이해하면 될 것이다.  
또한 각 패턴들은 범위에 따라 디자인 패턴으로 사용될 수도 있고 아키텍처 패턴으로 사용될 수도 있으며, 안드로이드 분야에서 자주 언급되는 MVC, MVP, MVVM 패턴은 **아키텍처 패턴이라고 하는 게 더 정확하다고 볼 수 있다.**

<br/>

## MVC 패턴 계층
| 계층 | 설명 |
| --- | --- |
| Model | 애플리케이션에서 데이터를 저장하고 처리하는 계층을 의미한다. |
| View | 애플리케이션에서 사용자가 직접 보는 화면(UI)을 담당하는 계층을 의미한다. |
| Controller | 뷰와 모델 간의 관계를 설정하는 계층이며 해당 부분에서 애플리케이션의 로직을 담당하는 계층을 의미한다. (View에서 UI를 갱신하고 Model에서는 데이터를 업데이트 하는 구조다.) |

<br/>

## MVC 아키텍처 패턴의 흐름 : 전체 흐름
사용자의 Action → Controller → Model → Controller → View → Controller → View → 사용자 화면

<br/>

## MVC 아키텍처 패턴의 흐름 : 상세 흐름
1. 사용자의 Action을 Controller에서 받는다. (사용자 Action → Controller)
2. Controller에서는 이를 확인하고 Model을 업데이트 수행한다. (Controller → Model)
3. 수정된 값을 Controller로 반환한다. (Controller ← Model)
4. Controller에서는 View를 수정한다. (View ← Controller)
5. 사용자에게 변경된 화면을 반환한다. (사용자 Action ← View)

<br/>
<br/>

# ✅ MVC 패턴의 각 컴포넌트의 역할(Who, When, What) 및 규칙
## Controller(컨트롤러)
- 일종의 조정자라고 할 수 있다. 클라이언트의 요청을 받았을 때, 그 요청에 대해 실제 업무를 수행하는 모델 컴포넌트를 호출한다. 또한 클라이언트가 보낸 데이터가 있다면, 모델에 전달하기 쉽게 데이터를 가공한다. 모델이 업무를 마치면 그 결과를 뷰에게 전달한다.
- 사용자가 접근한 URL에 따라 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를 Model을 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려 준다.
- 모델에 명령을 보냄으로써 뷰의 상태를 변경할 수 있다.    
    ex : 워드에서 문서 편집    
- 컨트롤러가 관련된 모델에 명령을 보냄으로써 뷰의 표시 방법을 바꿀 수 있다.    
    ex : 문서를 스크롤하는 것
    
<br/>

### 컨트롤러의 규칙
- 모델이나 뷰에 대해서 알고 있어야 한다.
- 모델이나 뷰의 변경을 모니터링해야 한다.

<br/>

## Model(모델)
- 컨트롤러가 호출할 때, 요청에 맞는 역할을 수행한다. 비즈니스 로직을 구현하는 영역으로 응용 프로그램에서 데이터를 처리하는 부분이다. `비즈니스 로직`이란 업무에 필요한 데이터 처리를 수행하는 응용 프로그램의 일부라고 할 수 있다. DB에 연결하고 데이터를 추출하거나 저장, 삭제, 업데이트, 변환 등의 작업을 수행한다. 상태의 변화가 있을 때 컨트롤러와 뷰에 통보해 후속 조치 명령을 받을 수 있게 한다.
- 데이터를 가진 객체를 모델이라고 지칭한다. 데이터는 내부의 상태에 대한 정보를 가질 수도 있고, 모델을 표현하는 이름 속성으로 가질 수 있다. 모델의 상태에 변화가 있을 때 컨트롤러와 뷰에 이를 통보한다. 이와 같은 통보를 통해 뷰는 최신의 결과를 보여 줄 수 있고, 컨트롤러는 모델의 변화에 따른 적용 가능한 명령을 추가, 제거, 수정할 수 있다.

<br/>

### 모델의 규칙
- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야만 한다.
- 뷰나 컨트롤러에 대해서 어떠한 정보도 알지 말아야 한다.
- 변경이 일어나면 변경 통지에 대한 처리방법을 구현해야 한다.

<br/>

## View(뷰)
- 컨트롤러로부터 받은 모델의 결과 값을 가지고 사용자에게 출력할 화면을 만드는 일을 한다. 만들어진 화면을 웹 브라우저에 전송하여 웹 브라우저가 출력하게 하는 것이다. 화면에 표시되는 부분으로 추출한 데이터나 일반적인 텍스트 데이터를 표시하거나 입력 폼 또는 사용자와의 상호작용을 위한 인터페이스를 표시하는 영역이다.
- View는 클라이언트 측 기술(웹에서는 HTML/CSS/Javascript)들을 모아 둔 컨테이너이다. 사용자가 볼 결과물을 생성하기 위해 모델로부터 정보를 얻어온다.

<br/>

### 뷰의 규칙
- 모델이 가지고 있는 정보를 따로 저장해서는 안 된다.
- 모델이나 컨트롤러와 같이 다른 구성 요소를 몰라야 한다.
- 변경이 일어나면 변경 통지에 대한 처리 방법을 구현해야 한다.

<br/>
<br/>

# ✅ MVC 구동 원리(How)
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJeqRn%2FbtqID6bWwwA%2FLcgEx13rMmHLWwGzkftTwK%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJeqRn%2FbtqID6bWwwA%2FLcgEx13rMmHLWwGzkftTwK%2Fimg.png)

C/S(Client - Server) 구조로 요청을 하면 그에 맞는 응답을 하는 구조를 기본으로 하고 있다.
1. 웹 브라우저가 웹 서버에 웹 애플리케이션 실행을 요청한다. (MVC 구조가 WAS라고 보면 된다.)
2. 웹 서버는 들어온 요청을 처리할 수 있는 서블릿을 찾아서 요청을 전달한다. (Matching)
3. 서블릿은 모델 자바 객체의 메서드를 호출한다.
4. 데이터를 가공하여 값 객체를 생성하거나, JDBC를 사용하여 데이터베이스와의 인터랙션을 통해 값 객체를 생성한다.
5. 업무 수행을 마친 결과 값을 컨트롤러에게 반환한다.
6. 컨트롤러는 모델로부터 받은 결과 값을 View에게 전달한다.
7. JSP는 전달받은 값을 참조하여 출력할 결과 화면을 만들고 컨트롤러에게 전달한다.
8. 뷰로부터 받은 화면을 웹 서버에게 전달한다.
9. 웹 브라우저는 웹 서버로부터 요청한 결과 값을 응답받으면 그 값을 화면에 출력한다.

<br/>
<br/>

# ✅ MVC 패턴 방식
MVC 패턴에는 Model 1 방식과 Model 2 방식이 있다.
- Model 1 방식 : JSP에서 출력과 로직을 전부 처리
- Model 2 방식 : JSP에서 출력만 처리

<br/>

## Model 1 방식
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw08Lw%2FbtrlbKqhWKO%2FqUYnM7xziHIQUE28L6WBZ1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fw08Lw%2FbtrlbKqhWKO%2FqUYnM7xziHIQUE28L6WBZ1%2Fimg.png)

Controller와 프레젠테이션 영역(View)을 같이 구현하는 방식이다.  
사용자의 요청을 JSP가 전부 다 처리한다. 웹 브라우저 사용자의 요청을 받은 JSP는 자바빈이나 서비스 클래스를 사용하여 웹 브라우저가 요청한 작업을 처리하고 그 결과를 출력해 준다.

<br/>

## Model 2 방식
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGZKd4%2FbtrleqFoykC%2FkXkFFucLJdHJ4hNvfcmav0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGZKd4%2FbtrleqFoykC%2FkXkFFucLJdHJ4hNvfcmav0%2Fimg.png)

Controller와 프레젠테이션 영역이 분리되어 있는 구현 방식이다.  
웹 브라우저 사용자의 요청을 Servlet이 받는다. Servlet은 요청을 View로 보여줄 것인지, Model로 보내줄 것인지 정하여 전송한다. 여기서 View 페이지는 사용자에게 보여주는 역할만 담당하고 실질적인 기능의 부분은 Model에서 담당한다.  
또한 Model  2 방식의 경우 HTML 소스와 JAVA 소스를 분리해 놓았기 때문에 Model 1 방식에 비해 확장시키기도 쉽고 유지보수 또한 쉽다.

<br/>

## Model 1 방식  vs  Model 2 방식
|  | Model 1 방식 | Model 2 방식 |
| --- | --- | --- |
| 장점 | 빠르고 쉽게 개발 가능 | 디자이너와 개발자의 분업이 가능하며 유지보수 및 확장이 쉬움 |
| 단점 | JSP 파일이 너무 비대해지며 Controller와 View가 혼재하므로 향후 유지보수에 어려움 | 설계가 어려우며 개발 난이도가 높음 |
> Model 1 방식으로 웹 서비스를 개발하는 사례는 백엔드와 프론트엔드의 역할 분담이 모호해져 협업이 쉽지 않으며 실제 서비스들 중에서 거의 없다고 봐도 무방하다.
> 

<br/>
<br/>

# ✅ MVC 패턴 특징
- 애플리케이션을 세 부분으로 분리함으로써 더 이해하기 쉬워지고 부속 간의 의존성이 낮아진다.
- 개발자들이 각각 특정 로직 코드에만 집중할 수 있도록 업무를 분할할 수 있다.
- 로직에 영향을 주지 않고 화면 표시를 수정할 수 있다.
- 화면 표시에 영향을 주지 않고 로직을 수정할 수 있다.
- 뷰를 수정하지 않고 사용자 동작에 반응하는 코드를 수정할 수 있다.

<br/>
<br/>

# ✅ MVC 패턴 장단점
## MVC 패턴 장점
- 유연하고 확장하기 쉽다.
- 디자이너와 개발자의 협업이 용이하다.
- 유지보수 비용을 절감할 수 있다.

<br/>

## MVC 패턴 단점
- 기본 기능 설계를 위해 클래스들이 많이 필요하기 때문에 복잡할 수 있다.
- 설계 시간이 오래 걸리고 숙련된 개발자가 필요하다.
- Model과 View의 완벽한 분리가 어렵다.
> Model과 View의 의존성이 완벽히 분리 할 수 없기 때문에 패턴이 모호해질 수 있고 변형이 올 수 있다.
> 

> Model과 View가 서로에 대한 정보를 가지고 있지 않고 독립적이라고는 하지만, 다수의 Model과 해당하는 다수의 View가 하나의 Controller를 통해 소통을 이루고 있기 때문에 Model 과 View의 의존성이 완전히 분리될 수는 없다.  
따라서 Controller 하나에 다수의 Model과 View가 복잡하게 연결되어 있는 상황이 생길 수 있다. 이러한 Model과 View의 의존성 문제를 해결하기 위해 나온 MVC의 파생형 패턴 중 하나가 바로 MVVM 패턴이다.
> 

<br/>
<br/>

# ✅ MVC 패턴을 사용해야 하는 이유
- 사용자가 보는 페이지, 데이터 처리, 그리고 이 두 가지를 중간에서 제어하는 컨트롤, 이 세 가지로 구성되는 하나의 애플리케이션을 만들면 각각 맡은 바에만 집중할 수 있게 된다. 공장에서도 하나의 역할들만 담당하고 처리해서 **효율적이다.** MVC 패턴도 마찬가지다.
- 서로 분리되어 각자의 역할에 집중할 수 있게끔하여 개발을 하고 그렇게 애플리케이션을 만든다면 **유지보수성, 애플리케이션의 확장성, 그리고 유연성이 증가**하고, **중복 코딩이라는 문제점 또한 사라지게 된다.**
- 비즈니스 로직과 UI 로직을 분리하여 유지보수를 독립적으로 수행 가능하다.

<br/>
<br/>

# 🗂 참고
- [[개발상식] MVC 패턴이란? (Model-View-Controller) :: 코딩 공부 일지 (tistory.com)](https://cocoon1787.tistory.com/733)
- [[Android] 디자인 패턴, 아키텍처 패턴 (tistory.com)](https://jionchu.tistory.com/entry/Android-Design-Pattern-vs-Architectural-Pattern)
- [[Kotlin] 앱 아키텍처 패턴(MVC, MVP, MVVM) 이해하기 — 시작해볼래 (tistory.com)](https://adjh54.tistory.com/60)
- [MVC 패턴이란 무엇인가? (tistory.com)](https://osy0907.tistory.com/63)
- [MVC Pattern(Model, View, Controller) | 잡다한 IT 개발 이야기 (hwanine.github.io)](https://hwanine.github.io/others/MVC/)
- [MVC Pattern의 장단점 (tistory.com)](https://server-engineer.tistory.com/167)
- [[디자인패턴] MVC 패턴이란? : 네이버 블로그 (naver.com)](https://m.blog.naver.com/tlstjd436/222010976665)

