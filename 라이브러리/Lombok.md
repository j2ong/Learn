# Lombok

어노테이션 기반으로 코드를 자동완성 해주는 라이브러리이다.
Java 기반에서 기계적으로 작성하는 VO, DTO, Entity 관련 작업을 보다 쉽게 하게 해준다.

Getter, Setter, hasCode, ToString 같은 코드를 직접 소스를 작성하지 않고 어노테이션을 붙여서 같은 기능을 동작하게 할 수 있다.

Spring(SpringSTS) 프로젝트에서 사용할 경우 JPA 환경과 함께 일관화 되고 가독성이 좋은 애플리케이션을 작성할 수 있다.

### Before)
```
public class NonLombokModel {
     private String name;
     private String age;
     private String address;
     
    public NonLombokModel(String name, String age, String address) {
        super();
        this.name = name;
        this.age = age;
        this.address = address;
    }
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public String getAge() {
        return age;
    }
 
    public void setAge(String age) {
        this.age = age;
    }
 
    public String getAddress() {
        return address;
    }
 
    public void setAddress(String address) {
        this.address = address;
    }
 
    @Override
    public String toString() {
        return "NonLombokModel [name=" + name + ", age=" + age + ", address=" + address + "]";
    }
 
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((address == null) ? 0 : address.hashCode());
        result = prime * result + ((age == null) ? 0 : age.hashCode());
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        NonLombokModel other = (NonLombokModel) obj;
        if (address == null) {
            if (other.address != null)
                return false;
        } else if (!address.equals(other.address))
            return false;
        if (age == null) {
            if (other.age != null)
                return false;
        } else if (!age.equals(other.age))
            return false;
        if (name == null) {
            if (other.name != null)
                return false;
        } else if (!name.equals(other.name))
            return false;
        return true;
    } 
}

```

### After)
```
import lombok.*;
 
//@Data로 사용 가능
@Getter
@Setter
@ToString
@EqualsAndHashCode
@Builder
public class LombokModel {
     private @NonNull String name;
     private @NonNull String age;
     private @NonNull String address;
     
}

```


[Lombok 어노테이션](https://mangkyu.tistory.com/78)  

[소스참고](https://niceman.tistory.com/99)