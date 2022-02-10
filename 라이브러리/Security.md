# Security

스프링 기반의 애플리케이션의 보안(인증과 권한, 인가 등)을 담당하는 스프링 하위 프레임워크이다. 즉 인증(Authenticate, 누구인지?) 과 인가(Authorize, 어떤것을 할 수 있는지?)를 담당하는 프레임워크를 말한다.

보안과 관련해서 체계적으로 많은 옵션을 제공해주기 때문에 개발자 입장에서 일일이 보안관련 로직을 작성하지 않아도 된다는 장점이 있다.

기본용어

- 접근 주체(Principal) : 보호된 리소스에 접근하는 대상
- 인증(Authentication) : 보호된 리소스에 접근한 대상에 대해, 작업을 수행해도 되는 주체인지 확인하는 과정   
**=>  즉, 누구인지?**
- 인가(Authorize) : 해당 리소스에 대해 접근 가능한 권한을 가지고 있는지 확인하는 과정(After Authentication, 인증 이후)    
**=> 즉, 어떤 것을 할 수 있는지?** 
- 권한 : 어떠한 리소스에 대한 접근 제한, 인가 과정에서 해당 리소스에 대한 제한된 최소한의 권한을 가졌는지 확인
     
---
시큐리티 라이브러리가 작동하게되면
홈페이지 어느 곳을 가던지 시큐리티가 가로챈다.  
   
<img src="https://user-images.githubusercontent.com/68761119/152897152-84a69f25-046f-4274-978a-5b11c66cf8a3.png" width="220" height="150"/>

---
# 사용방법
## pom.xml
```
<!-- 시큐리티 태그 라이브러리 -->
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-taglibs</artifactId>
		</dependency>

<!-- 스프링에서 시큐리티를 사용할 수 있게 해주는 라이브러리 -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
			<version>2.6.1</version>
		</dependency>

```

## JSP  
JSP 파일에서 태그 라이브러리를 추가
```
<%@ taglib prefix="sec" uri="http://www.springframework.org/security/tags"%>
```

JSTL처럼 사용할 수 있다.
```
<!-- 표현식이 지정한 권한에 맞을 때만 출력 -->
<sec:authorize access="isAnonymous()">
   로그인
   회원가입
</sec:authorize>

<sec:authorize access="isAuthenticated()">
   로그아웃
   회원정보보기
</sec:authorize>

<sec:authorize access="hasRole('admin')">
  관리자 페이지
</sec:authorize>
```

---

![x](https://user-images.githubusercontent.com/68761119/152896348-f1bcb5f3-36fd-4d44-abf8-ef9bc223151a.png)

![y](https://user-images.githubusercontent.com/68761119/152896346-c7f4d72d-6c96-41bd-b328-89b5524e35cb.png)

인증에 성공한 경우

---  

표현식|설명|
|---|---|
hasRole('role')|해당 권한이 있을 경우|
hasAnyRole('role1,'role2')|포함된 권한 중 하나라도 있을 경우|
isAuthenticated()|권한에 관계없이 로그인 인증을 받은 경우|
isFullyAuthenticated()|	권한에 관계없이 인증에 성공했고, 자동 로그인이 비활성인 경우 |
isAnonymous()|권한이 없는 익명의 사용자일 경우|
isRememberMe()|자동 로그인을 사용하는 경우|
permitAll|모든 경우 출력함|
denyAll|모든 경우 출력하지 않음|




---

[표현식](https://docs.spring.io/spring-security/site/docs/4.2.x/reference/html/el-access.html#el-access-web)  

[참고](https://codevang.tistory.com/272)