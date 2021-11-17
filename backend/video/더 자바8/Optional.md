# Optional

## Optional 소개

- 기존 객체의 null 처리 방법
```java
public class App {
    public static void main(String[] args) {
        List<OnlineClass> springClasses = new ArrayList<>();
        springClasses.add(new OnlineClass(1, "spring boot", true));
        springClasses.add(new OnlineClass(2, "spring data jpa", true));
        springClasses.add(new OnlineClass(3, "spring mvc", false));

        OnlineClass spring_boot = new OnlineClass(1, "spring boot", true);
        Progress progress = spring_boot.getProgress();
        if (progress != null) {
            System.out.println(progress.getStudyDuration);
        }
    }
}
```
우리는 사람이기 때문에 `progress`같은 객체의 null 체크를 깜빡할 수 있다. <br>
그러기에 종종 당연히 `NullPointerException`을 종종 볼 수 있다.<br>

메소드에서 작업 중 특별한 상황에서 값을 제대로 리턴할 수 없는 경우 선택할 수 있는 방법
- 예외를 던진다. (비싸다, 스택트레이스를 찍어두니까)
- null을 리턴한다. (비용 문제가 없지만 그 코드를 사용하는 클라이언트 코드가 주의해야 한다.)
- (자바 8부터) Optional을 리턴한다. (클라이언트의 코드에게 명시적으로 빈 값일 수도 있다는 걸
  알려주고, 빈 값인 경우에 대한 처리를 강제한다.)

Optional
 - 오직 값 한 개가 들어있을 수도 없을 수도 있는 컨테이너.

주의할 것
- 리턴값으로만 쓰기를 권장한다. (메소드 매개변수 타입, 맵의 키 타입, 인스턴스 펠드 타입으로 쓰지말자)
- Optional을 리턴하는 메소드에서 null을 리턴하지 말자.
- 프리미티브 타입용 Optional이 따로 있다. OptionalInt, OptionalLong...
