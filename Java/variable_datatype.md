# 변수
### 변수와 메모리의 관계는?
    
    변수는 메모리 공간에 이름을 붙여주는 것이다.
    
    변수를 선언하면, 메모리의 빈 공간에 ‘변수타입’에 알맞은 크기의 저장공간이 확보되고,
    앞으로 이 저장공간은 ‘변수이름’을 통해 사용할 수 있게 된다.
    
### 변수의 이름이 길면 메모리를 많이 차지할까?
    
    컴파일 언어같은 경우 컴파일러가 모든 변수 이름을 메모리 주소와 CPU 레지스터 등으로 교체하기 때문에 변수의 길이는 메모리와는 상관이 없다.
    
    자바 같은 중간단계 언어로 변환하는 언어의 경우 변수 이름, 메소드 이름, 클래스 이름 등은 중간 단계 언어로된 코드(바이트 코드)에 남아 있다.
    그러나 난독화 과정을 거치면 난독화 기기가 모든 변수들은 짧은 이름으로 변환하므로 긴 이름은 상관 없어진다.
    
    - 자바는 왜 변수 이름이 컴파일 후에도 여전히 남아있을까?
        
        
### 변수의 이름이 길면 성능에 영향을 미칠까?
### 왜 변수 이름 첫 문자에는 유니코드, 알파벳, $, _ 만 사용가능할까?
    
    그 외의 것들은 대부분 연산자로 사용되고나 특별한 문법적 의미가 있어서,
    변수 이름으로 사용되면 혼동을 일으킬 수 있다.
    
### 왜 변수 이름은 숫자로 시작할 수 없을까?
    
    int 123 = 47   int 0x13 = 58
    
    딱 봐도 무척 혼란스럽다.

# 자료형
### 기본 자료형이 따로 존재하는 이유는?
    효율성을 위해서다. 

    기본 자료형은 메모리에 그대로 저장되는 반면, 
    참조형은 실제 데이터가 들어 있는 곳의 주소를 저장한다.

    따라서 우리가 기본 자료형이 아닌 참조형을 사용한다면,
    실제 데이터가 저장된 메모리 공간과 이 메모리 공간의 주소가 저장된 메모리 공간이 필요하기 때문에 메모리 효율적이지 않다.
    또한 JVM이 실제 값을 찾기 위해서 메모리 주소 공간을 이용해 데이터를 찾는 과정이 필요하므로 곧바로 데이터를 찾는 것에 비해 효율적이지 않다.

    기본 자료형의 데이터들은 매우 자주 쓰이는 것들이기 때문에 위에 언급된 비효율성이 크게 작용하므로 기본 자료형이 따로 존재하는 것이다.
    
### String은 왜 기본 자료형이 아닐까?
    
    변수를 선언하면 그 변수는 비어 있는 메모리에 있는 특정 주소에 공간을 만든다.
    
    int형으로 선언할 경우 그 공간은 4byte의 크기를 갖는다.
    
    만약 String으로 선언한다면 몇 byte를 가져야 할까?
    
    String으로 올 수 있는 값은 크기가 변동적이기 때문에 이 값을 특정할 수 없다.
    
    예를 들어 String이 기본 자료형이고 String a = “hello”와 같이 선언했다고 해보자.
    
    a라는 값이 메모리 주소 0x11을 가르킨다고 하면, 다음과 같이 저장될 것이다.
    
    [  h  ][  e  ][  l  ][ l  ][  o  ]
    0x11 ... 
    
    이 때 a = “school과 같이 hello보다 더 긴 문자열을 재할당하면,
    a주소가 만들어 놓은 5바이트의 공간이 초과될 것이고 5바이트 공간 이후에 다른 값이 저장되어 있을 수 있는데 그런 값을 덮어씌우던지 등 여러모로 문제가 생길 것이다.
    
    대신에 String을 참조자료형으로 만든다면 언제나 실제 값의 주소만을 갖기 때문에,
    아무리 실제 값이 커지더라도 다시 그 데이터에 주소만 저장하면 되므로 문제가 없다.
    
### String은 왜 immutable할까?
    1. 보안
        
        String은 주로 중요한 정보에 많이 쓰인다.
        
        예를 들면 유저 이름, 패스워드, url 등등
        
        만약 어떤 유저가 회원가입할 때 우리가 여러가지 체크를 통해서 제출된 이름이 규칙에 걸맞다는 것을 확인했다고 하자.
        
        만약 String이 mutable하다면, 이렇게 삼엄한 체크가 이루어진 후에도 안심할 수 없다.
        
        이 String의 레퍼런스를 갖고 있는 쪽이 database에 집어넣기 전에 String에 어떠한 변화를 줄 수도 있기 때문이다.(프로그램 바깥에서 어떻게 이 String을 변화시키는지는 잘 몰겠다.)
        
        하지만 String이 immutable하다면, 우리는 securiy check가 끝나면 안심하고 이 String을 다룰 수 있다.
        
    2. 성능
        
        자바에서 String은 String pool에 저장된다. 동일한 String을 사용하는 변수들이 String pool에 있는 하나의 데이터를 가르키게 하여 메모리를 절약한다.
        
        이 때 String이 mutable하다면 String이 변경됐을 때 이 String을 가르키는 모든 변수가 원치않는 변화로 피해를 입을 것이다.
        
        즉 String pool이라는 기능이 가능한 것은 String이 immutable하기 때문이다.
        
        또한 String은 HashMap이나 HashSet의 자료 구조에서 key로 많이 쓰이게 된다.
        
        String이 immutable하기 때문에 String constant pool에 있는 String들은 한 번 hashCode()가 호출되면 그 값을 캐싱하고 있다가 다시 한 번 호출될 때는 caching한 값을 반환하기 때문에 자료구조에서 데이터를 찾을 때마다 haschCode()의 연산 과정이 필요없어서 성능상 이점을 준다.
        
### String a = “hello” 와 String a = new String(”hello”) 의 차이는 뭘까?
    
    String a = “hello”와 같이 스트링을 만들어 줄 경우,
    이 “hello”라는 데이터는 heap안에 있는 “String constant pool”이라는 곳에 저장된다.
    
    이렇게 선언해 놓으면, 다음 번에 String b = “hello”와 같이 동일한 문자열을 선언할 경우,
    새롭게 메모리 영역에 데이터를 할당하는게 아니라 String constant pool”에서 동일한 데이터가 이미 존재하는지 찾고, 있다면 그 데이터의 주소를 b에 할당해준다.
    
    따라서 다음이 성립한다.
    
    String a = "hello";
    String b = "hello";
    
    a == b // true
    
    반면에 new 키워드로 스트링을 생성할 경우 이 데이터는 heap 영역 안에 “String constant pool” 밖에 저장된다.
    
    동일한 문자열을 다시 new로 생성하면 동일한 데이터를 heap 안에 새로운 영역에 또 할당한다.
    
    따라서 다음이 성립한다.
    
    String a = new String("hello");
    String b = new String("hello");
    
    a == b // false
    
    - String constant pool도 가비지 컬렉팅이 작동할까?
        
        String constatnt pool도 heap 영역 안에 있기 때문에 더 이상 접근 불가한 String들은 가비지 컬렉팅된다.
        
        Java 7 이전에는 특별한 heap 영역인 PermGen이라는 곳에 String constant pool이 위치해서 가비지 컬렉팅이 작동하지 않았다.
        
        그러나 Java 7 이후에는 메인 heap 영역으로 옮겼기 때문에 가비지 컬렉팅이 작동한다.
        
        참고로 Java 8 이후에는 PermGen을 Metaspace라는 녀석이 대체했다.
        
### 왜 (byte)(127 + 2)는 -127 일까?
    
    컴퓨터는 이진수로 계산하고 byte는 8비트이다.
    
    127은 01111111이고 2를 더하면 10000001이 된다.
    
    자바는 2의 보수법을 이용하여 정수들을 표현하고 byte타입도 마찬가지다.
    
    이 말은 음수를 표현할 때 그 숫자와 절대값이 같은 양수의 2의 보수로써 표현한다는 것이다.
    
    예를 들면 -1은 1에 대한 2의 보수, -5는 5에 대한 2의 보수이다.
    
    10000001은 127(01111111)에 대한 2의 보수이다. 따라서 -127이다.
    
    - 2의 보수란?
        
        먼저 보수란 ‘보완해주는 수’라고 할 수 있다.
        컴퓨터가 계산할 대 덧셈과 뺄셈을 간편하게 하기 위해서 고안되었다.
        
        n비트의 수가 있을 때 이 수의 2의 보수란,
        이 수와 더해서(보완해서) 2^n이 나오는 수이다.
        
        예를 들어 byte의 경우 8비트이다.
        
        8비트 숫자 1이 있을 때 이 숫자는 00000001로 표현된다.
        
        숫자 00000001이 2^8인 100000000이 되기 위해서는 11111111과 더해져야 한다.
        
        따라서 8비트 숫자 00000001의 2의 보수는 11111111이다.
        
        둘을 더하게 되면 100000000이 나오고 8비트까지만 표현되기 때문에,
        처음 1은 잘리고 00000000 , 즉 0이 된다.
        
        이렇게 1 -1 = 0 이 되는 것이다.
        
### 어떻게 float이나 double은 같은 byte크기일 때 정수형보다 훨씬 큰 값을 표현할 수 있을까?
    
    값을 저장하는 형식이 다르기 때문이다.
    
    float은 178이라는 값이 있으면 대략적으로 다음과 비슷한 방식으로 저장한다.
    
    1.78 x 10^2 → 178과 2라는 값을 저장 
    
    int값의 최대값보다 큰 50억이라는 값은 float에 어떻게 저장할 수 있을까?
    
    5 x 10^9 → 5와 9라는 값을 저장
    
    정확한 방식은 아니지만 대략 이런 식으로 float과 double이 int와 double보다 큰 값을 저장할 수 있다. 대신에 이런 방식은 특정 범위를 넘으면 오차가 발생한다.
    
### 왜 float과 double은 돈 계산과 같이 정확한 계산이 요구될 때 사용하면 안될까?
    
    10진수 10.1을 float에 저장한다고 해보자.
    
    첫째로 10.1을 2진수의 형태로 변환해야 한다.
    
    정수 10과 소수 0.1을 따로 변환환다.
    
    [  1  ] [  0  ] [  1  ] [  0  ]  = 10의 2진 표현
      2^3     2^2     2^1     2^0
    
    [  0  ] [  0  ] [  0  ] [  1  ] [  1  ] ...  = 0.1의 2진 표현
      2^-1    2^-2    2^-3    2^-4    2^-5
    
    10.1 = 1010.00011.... 
    
    0.1이 2진수로 표현하는 과정에서 무한소수가 되어버리기 때문에 0.1을 2진법으로 정확하게 표현할 수 없고 근사해서 표현할 수 밖에 없다.
    
    이러한 과정에서 오차가 생긴다.
    
### float은 7정밀도 라는 것이 무슨 말일까?
    
    이 말은 132.4875 이런식으로 7자리의 이하의 수는 무조건 오차없이 표현할 수 있다는 말이 아니다.
    
    float이 표현할 수 있는 수들은 약 10^-7의 오차 안에서 정확하게 표현될 수 있다는 말이다.
    
    그렇다고 모든 수가 오차가 있는 것은 아니고, 
    10같은 경우 정확하게 표현할 수 있으며 10.1은 2진수로 변환시 0.1이 무한소수가 되어 오차가 발생한다.
    
### float은 왜 이름이 float이고 double은 왜 이름이 double일까?
    
    float은 실수값을 부동소수점(floating-point)방식으로 저장하기 때문에 float이다.
    
    double은 float보다 두 배의 크기(8 byte)를 갖고 2배 더 정밀하기 때문에 double이다. 
    
### 왜 지역변수는 초기화를 안했을 때 기본값이 정해지지 않을까?
    
    사실 초기화 안했을 때 디폴트라는 값을 주는 것보다, 
    지역변수에게 그렇듯, 사용 전에 초기화 안된 변수는 컴파일러가 허용하지 않는 것이 좋다. 우리는 대부분 변수를 초기화해서 사용하고, 변수를 초기화하지 않은 채로 변수를 사용하는 것은 대부분 의도되지 않은 일로써, 이러한 과정에서 발생한 에러를 컴파일 타임에서 잡을 수 있기 때문이다.
    
    지역변수가 초기화되지 않았는지는 그 메소드만 보면 알 수 있다.
    따라서 초기화하지 않은 변수는 반드시 초기화되지 않은 채로 읽혀질 것이라는 것을 컴파일러는 확실 할 수 있고 이 부분을 컴파일러가 잡아줄 수 있다. 
    
    그러나 인스턴스 변수나 스태틱 변수는 초기화를 하지 않았다고 해서 이 값이 사용되기 전에  초기화되지 않을 것이라는 것을 그 클래스만 봐서는 컴파일러가 확신할 수 없다.
    왜냐하면 선언할 때는 초기화 안했지만 그 후에 값을 읽기 전에 setter를 이용해 초기화할 수도 있기 때문이다.
    
    따라서 컴파일러가 선언시 초기화하지 않은 인스턴스나 스태틱 변수에 대해서 컴파일 에러를 뿜지 않고 기본값을 할당함으로써 우리의 실수를 방지하게 도움을 주는 것이다.
    
    나름대로 컴파일러가 최선을 다했다고 볼 수 있다. 
    
### 왜 int는 정수 literal의 기본 자료형이고 double은 실수 literal의 기본 자료형일까?
    - 정수 literal이 기본적으로 int로 취급되는 이유.
        
        자바가 처음 나오던 시절에 대부분의 컴퓨터는 32비트 아키텍처였다.
        
        따라서 long을 기본형으로 쓰게 되면 계산할 때마다 32비트 레지스터를 2개 써야하기 때문에 효율적이지 않았다.
        
        그래서 정수 literal에 long보다는 int가 기본적으로 쓰였지 않나 싶다.. 
        
        지금 시대에는 long을 쓰는 것이 더 효율적이지만,
        기본형을 이제와서 long으로 바꾸면 자바로 만들어진 수많은 프로그램들의 호환성을 보장할 수 없기 때문에 int를 유지하는 것 같다.
        

    - 실수 literal이 기본적으로 double로 취급되는 이유.
        
        만약 float이 기본형이라면 다음과 같은 문제가 있을 것이다.
        
        double d = 0.1;
        
        double d2 = 0.1d;
        
        d == d2일 것 같지만 0.1은 float으로 처리되기 때문에 정밀도에서 이미 손실을 본 상황이라
        d ≠d2이다. 즉 프로그래머의 의도와는 다르게 되므로 언어설계적으로 좋지 않은 발상이다.
        
        double이 기본형이라면 문제가 없다.
        
        실수에 대해서는 효율보다는 이러한 부분을 더 중점적으로 보지 않았을까..?