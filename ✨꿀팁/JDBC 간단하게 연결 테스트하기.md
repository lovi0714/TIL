#java #jdbc #테스트

프로젝트 중에 JDBC 연결 확인을 부탁하셔서 직접 해봤다.
batch 개발하려는 서버에서 테스트가 필요했다.

#### 1. 자바 파일 작성
	리눅스 서버여서 , vi로 간단한 코드를 작성했다.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class TestDBConnection {
    public static void main(String[] args) {

        // Oracle Database connection details
        String jdbcUrl = "jdbc:oracle:thin:@db_host:1521/서비스 이름";
        //String jdbcUrl = "jdbc:oracle:thin:@db_host:1521/SID 이름";
        String username = "아이디";
        String password = "비밀번호";

        try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {
            if (connection != null) {
                System.out.println("성공");
            } else {
                System.out.println("실패");
            }
        } catch (SQLException e) {
            System.out.println("error: " + e.getMessage());
        }
    }
}
```

#### 2. 컴파일
	그 다음 오라클 jdbc 드라이버가 필요하니까, 경로 지정해주고 컴파일 해준다.

```bash
javac -cp /경로/ojdbc8.jar TestDBConnection.java
```

#### 3. 실행

	그리고 컴파일 된 class 파일을 실행해주면 끝

```bash
java -cp .:/경로/ojdbc8.jar TestDBConnection
```


테스트 해본 결과 타임 아웃이 발생했다.
추가적으로 ping이랑 telnet 써서 확인해봤는데 연결이 안 되는 것 같았다.

여기서 중요한 점은 url 설정하는 곳에서 

 >[!note]
	String jdbcUrl = "jdbc:oracle:thin:@db_host:1521/서비스 이름";  
	String jdbcUrl = "jdbc:oracle:thin:@db_host:1521:SID 이름";

서비스 이름과 SID 이름을 사용할 때 
`/` 와 `:` 의 차이가 있다. 주의할 것!