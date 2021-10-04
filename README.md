# Spring-java-get-post-hangle-parameter-check
Spring Get /Post 한글 파라미터 값 깨짐 현상

>>한글 깨짐 원인은 tomcat 또는 프로젝트 파일 web.xml 파일 설정과 연결되어 있다.
>>그리고 적용 방식에는 POST 방식과 GET 방식에 따라 달라진다.

## POST 방식 일 경우
-> WEB-INF/web.xml
  * 해당 프로젝트 web.xml 에 filter 기능을 추가 한다.

```C
  <filter>
  <filter-name>encodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <init-param>
   <param-name>encoding</param-name>
   <param-value>UTF-8</param-value>
  </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

## GET 방식 일 경우
-> tomcat -> server.xml
 * GET 방식일 경우 한글 데이터를 받기 위해서는 서버 내에 직접 설정이 필요하다.
 * 톰켓 하위 server.xml 안에 아래 코드를 찾아 URIEncoding="UTF-8"을 추가한다.
 ```C
    <Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="UTF-8"/>
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" URIEncoding="UTF-8"/>
 ```
