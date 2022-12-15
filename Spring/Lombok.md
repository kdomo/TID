### Lombok 이란?

자바의 보일러 플레이트(boilerplate) 코드를 줄여주는 라이브러리

### Lombok의 기능

- `@Setter`, `@Getter` : Java Bean 규약에 있는 setter, getter를 자동 생성
- `@ToString` : Object에 기본 구현된 ToString 대신 객체의 데이터를 보여주는 ToString을 자동 생성
- `@NoArgsConstructor`, `@AllArgsConstructor`, `@RequiredArgsConstructor `: 객체 생성자를 자동
으로 생성
- `@Data` : Getter, Setter, ToString, Equals, hashCode 등 다양한 기능을 모두 제공
- `@Builder` : 빌더 패턴을 자동 생성하여 제공
- `@Slf4j` : 해당 클래스의 logger를 자동 생성
- `@UtilityClass` : static method만 제공하는 유틸리티 성격의 클래스들의 생성자를 private으로 만들어
서 객체 생성을 할 수 없도록 함