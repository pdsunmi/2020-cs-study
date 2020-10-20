# Spring Framework

* [Spring Web MVC](#Spring-Web-MVC)
  * Spring Web Application의 실행 흐름

</br>

## Spring Web MVC

### Spring Web Application의 실행 흐름

#### 1. Web Application이 실행되면 WAS에 의해 web.xml 로드
web.xml의 ContextLoaderListener이 ApplicationContext를 생성한다.  
ContextLoaderListener은 Servlet의 생명주기를 관리해준다.  
contextConfigLocation 파라미터 설정을 통해 설정파일들을 로드할 수 있다.  
`<listener>`를 이용하여 두 DispatcherServlet의 공통 빈을 설정할 수도 있다.  

#### 2. 파라미터에 해당하는 root-context.xml 로드
root-context.xml을 로드하여 root 컨테이너를 구동한다. (Back-end와 관련된 설정을 담당)  
Business Logic에 대한 부분과 DAO, VO 객체들이 생성된다.  

#### 3. Web Browser(Client)로부터 request가 들어온다.
최초 Client 요청에 의해 DispatcherServlet이 생성된다.  
servlet-context.xml 을 로드하여 두번째 스프링 컨테이너를 구동한다. (웹과 관련된 설정 담당)  

#### 3. DispatcherServlet이 FrontController의 역할을 수행한다.
request에 대한 일을 누가 처리할 지(해당 request를 매핑한 컨트롤러가 있는지) `Handler Mapping`에 묻고 답을 얻는다.  
`Handler Adapter`에게 Controller를 불러달라고 요청하고 처리하여 `Controller`는 View에 전달할 자료들은 Model에 담고 결과를 출력할 View 이름을 반환한다.  
`ViewResolver`에게 이름 기반으로 결과를 보여줄 View를 문의하고 위치를 받는다.  
`View`에게 화면 표시를 요청한다.
