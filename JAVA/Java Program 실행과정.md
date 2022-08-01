# Java Program 실행과정
<p align="center"><img src="https://user-images.githubusercontent.com/64088250/182137354-440730b5-c2b8-4a41-a8bb-b8cf975e1ab5.jpg"></p>

- Java언어로 프로그래밍된 파일을 Java컴파일러가 가상 기계어 파일인 Java클래스 파일로 만든다. 다시 말해, 소스 코드를 Java바이트 코드로 번역한다. 이후 Java바이트 코드를 JVM이 읽고 실행하게 된다.

---

#### 바이트 코드란?
- JVM이 이해할 수 있는 언어로 변환된 자바 소스 코드를 의미한다. 자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 1바이트라서 자바 바이트 코드라고 불린다. 이러한 자바 바이트 코드의 확장자는. class이며 자바 바이트 코드는 자바 가상 머신만 설치되어 있으면, 어떤 운영체제에서 라도 실행될 수 있다.



#### JVM이란?
<p align="center"><img src="https://user-images.githubusercontent.com/64088250/182137959-ca67a40a-28e8-4e02-89b5-61d401b81788.jpg"></p>
- JVM은 JavaVirtual Machine의 줄임말로 wirte once, run erveywhere 즉 OS마다 따로 코드를 작성해야 하는 번거로움 업이 Java가 플랫폼에 독립적일 수 있게 만들어준다. 예를 들어 C 프로그램은 바로 기계어로 컴파일하므로 HW 기종에 맞게 컴파일되어야 한다. 이를 '플랫폼에 종속적'이다. 라고 한다. 반면 Java 프로그램은 중간 단계 언어로 컴파일하여 JVM만 각 OS만 설치되어 있다면 HW 기종에 상관없이 단 한 번만 컴파일하면 된다. 이를 '플랫폼에 독립적'이라고 한다. 간단히 말해 JVM은 Java 클래스 파일을 로드하고 바이트 코드를 해석하며, 메모리 등의 자원을 할당하고 관리하며 정보를 처리하는 작업을 하는 프로그램이다.

<p align="center"><img src="https://user-images.githubusercontent.com/64088250/182138084-3c2081f1-7da9-451c-868b-eb59c78cbb8f.jpg"></p>

- JRE는 자바 API와 JVM으로 구성되며, JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 들여서 자바 API와 함께 실행하는 것임.
- 자바 프로그램을 컴파일하면, JVM은 클래스 로더를 이용해서 컴파일된 바이트 코드를 메모리로 읽어들인다.
class Loader에 의해 바이트코드가 런타임 데이터 영역(Runtime Data Area)에 올라가게 되면 
실행 엔진(Execution Engine)이 바이트코드를 한줄씩 실행시킨다. 이 과정 속에서 JVM은 필요에 따라 garbage collection 등의 작업을 수행하게 된다.
- JVM의 메모리 구조는 활용 용도에 따라 여러 영역으로 구분되어 있는데, 메소드, 스택, 힙 영역이 프로그래밍과 관련이 있다.
- 지정된 클래스에서 main(String[] args)를 호출한다. 
Java Compiler 는ava Source파일을 JVM이 해석할 수 있는 Java Byte Code(. class)로 변경한다. 일반적인 윈도우 프로그램의 경우, Compile 이후 Assembly 언어로 구성된 파일이 생성된다.
- Class Loader는 JVM내로. class파일들을 Load 한다. Loading 된 클래스들을 Runtime Data Area에 배치된다. 일반적인 윈도우 프로그램의 경우 Load 과정은 OS가 주도한다.
- Execution Engine은 Loading 된 클래스의 Bytecode를 해석한다. 이 과정에서 ByteCode가 BinaryCode로 변경된다. 일반적인 윈도우 프로그램의 경우 Assembier가 Assembly언어로 쓰인 코드 파일을 BinaryCode로 변경한다.
- Runtime Data Area는 JVM이 프로세스로써 수행되기 위해 OS로부터 할당받는 메모리 영역이다. 저장 목적에 따라 다음과 같이 5개로 나눌 수 있다.
<br>

|Area|content
|:-------------:|:---|
|Method Area|모든 Thread에게 공유된다. 클래스 정보, 변수 정보, Method정보, static변수 정보, 상수 정보 등이 저장되는 영역|
|Heap Area|모든 Thread에게 공유된다. new 명령어로 생성된 인스턴스와 객체가 저장되는 구역, 공간이 부족해지면 Garbage Collection이 실행된다.
|Stack Area|각 스레드마다 하나씩 생성된다. Method안에서 사용되는 값들(매개변수, 지역변수, 리턴 값 등)이 저장되는 구역, 메서드가 호출될 때 LIFO로 하나씩 생성되고, 메서드 실행이 완료되면 LIFO로 하나씩 지워진다.
|PC Register|각 스레드마다 하나씩 생성된다. CPU의 Register와 역할이 비슷하다. 현재 수행 중인 JVM명령의 주소 값이 저장된다.
|Native Method Stack|각 스레드마다 하나씩 생성된다. 다른 언어(C/C++ 등)의 메서드 호출을 위해 할당되는 구역 언어에 맞게 Stack이 형성되는 구역이다. JNI(Java Native Interface)라는 표준 규약을 제공한다.