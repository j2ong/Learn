# Jstl
자바서버 페이지 표준 태그 라이브러리

JSTL은 JSP 페이지 내에서 자바 코드를 바로 사용하지 않고 로직을 내장하는(반복문, 조건문 등등)방법을 제공한다. 

표준화된 태그 셋을 사용하여 자바 코드가 들락거리는 것보다 더 코드의 유지보수와 응용 소프트웨어 코드와 사용자 인터페이스 간의 관심사의 분리로 이어지게 한다.

## JSTL의 사용법
JSTL은 라이브러리이기 때문에 사용하기전에 core를 header에 추가해주어야 한다.  
`<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>`

아래와 같이 사용할 수 있다.
```
 <c:choose>
    <c:when test = "${1 <= 0}">
            "1이 0보다 작습니다"
    </c:when>
    <c:otherwise>
            "그럴리가.."
    </c:otherwise>
</c:choose>
```      

[Core 태그들, 내장객체](https://daesuni.github.io/jstl/)  
[Tutorial](https://www.tutorialspoint.com/jsp/jsp_standard_tag_library.htm)
