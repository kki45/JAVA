## JAVA

- JDK(Java Development Kit) : jdk를 설치하면 jre와 jvm이 같이 설치되고 자바코드를 실행할수 있도록 도와준다.
- JRE(Java Runtime Environment) : jvm이 jre에 포함되어있다. jvm이 원활히 작동할 수 있도록 도와주는 환경이다.
- JVM(Java Virtual Machine) : 어떤 플랫폼이든 자바프로그램이 실행할 수 있도록 도와준다

### Class의 구성요소
1. Method와 Field이다.
2. main메소드를 가지는 클래스 앞에 public을 붙인다...다른클래스에는 붙이면 안된다
3. 

### static
1. static은 이미 메모리에 올라가있기때문에 메모리에 안올리고 바로 쓸수 있다.
2. 메모리에 올린다 == 객체를 생성한다.

### 생성자란? 
객체가 생성될 때마다 구동하는 것.

1. 모든 클래스에는 하나이상의 생성자가 무조건 존재한다.
2. 기본생성자는 개발자가 작성하지 않아도 무조건 클래스에 존재한다.

     Default Constructor는 인자값 X , { }구현부에서 아무런 일을 하지않는 생성자이다.
3. 명시적 생성자는 인자값이 하나이상이다. 하는일은 "필드 초기화"이다.
4.  클래스에 명시적 생성자를 작성해놓으면 컴파일러가 기본생성자를 넣어주는 작업을 하지않는다.
::
필드에 값이 주입되는 통로는 단 2개이다.
1) 명시적 생성자 :: 객체가 생성되는 것과 동시에 값이 주입된다.
2) setter( ) :: 객체가 생성된 직후에 값이 주입된다.

- 필드초기화 (this a = a;)

필드변수와 지역변수(로컬변수, 멤버변수)의 이름이 같을 때 구분하기 위해서 필드변수앞에 this를 붙여줌으로써 구분한다. 

명시적생성자에서 super키워드는 상위클래스를 가르키는 키워드이다.
부모클래스에서는 super();를 defalut로 한다.

### Has A Realtion
다른클래스의 기능을 받아 사용하는 것이다.
1. 필드레벨에 추가하고자하는 클래스를 선언.
2. 추가한 필드를 주입하는 통로를 하나 생성한다 --> 생성자 or setter( )

ex) Programmer가 Notebook을 가지는 관계를 설정한다.
```java
NoteBook.java

package com.edu.cons;

public class NoteBook {
	//필드선언
	public String brandName;
	public int price;
	public int serialNumber;
	
	public NoteBook() {//기본생성자
		
	}
	public NoteBook(String brandName, int price, int serialNumber) {//명시적생성자
		this.brandName = brandName;
		this.price = price;
		this.serialNumber = serialNumber;
	}
		public void printInfo() {//출력메소드
			System.out.println("NoteBook Brand :: "+brandName+", Price :: "+price+",Number ::"+ serialNumber);
		}

		public String getBrandName() {//브랜드이름출력메소드
			return "NoteBook brandName ::"+ brandName;
		}
		//메소드 추가.. 필드에 값을 할당받을수 있는 기능을 하나 추가한다.
		//brandname, price, serialnumber 위치가 메소드 영역안에 선언되어 있어 얘들은 local변수(지역변수, 인자값, 아큐먼트 리소스)라고 함.
		public void setNoteBookInfo(String brandName, int price, int serialNumber) {
			//~Test에서 기능호출 할 때 받은 인자값으로 다시 필드에 할당
			//필드초기화(Field initialization)
			
			//this:: 필드와 로컬변수의 이름이 같은 때 구분하기 위해 필드 앞에 붙혀준다.
			this.brandName = brandName;
			this.price = price;
			this.serialNumber = serialNumber;
		}

		}
```
```java
Programmer.java
package com.edu.cons;
//Programmer가 NoteBook을 가지는 관계를 설정...Has A Relation..
//다른 클래스의 기능을 받아 사용하는 것...Has A Relation..
/*
 * 1. 필드 레벨에 추가하고자 하는 클래스를 선언.
 * 2. 추가한 핃드를 주입하는 통로를 하나 생성
 *    생성자 혹은 setter()
 */
	public class Programmer {//클래스
	   String proName;
	   String proAddress;
	   String mainSkill;
	   int salary;
	   
	   NoteBook noteBook;//1.
	   
	   public Programmer() { } //기본생성자
	   public Programmer(String proName, String proAddress, String mainSkill, int salary) {//명시적생성자
		   this.proName = proName;
		   this.proAddress = proAddress;
		   this.mainSkill = mainSkill;
		   this.salary = salary;
	   }
	   //setter()를 추가
	   public void buyNoteBook(NoteBook noteBook) {
		   this.noteBook = noteBook;
	   }
	   //주입한 노트북을 다시 받아오는 루트 추가
	   public NoteBook getNoteBook() {
		   return noteBook;
	   }
	   public String getProgrammerInfo() {
	      return proName+"\t"+proAddress+"\t"+mainSkill+"\t"+salary;
	   }
	   
	   public void setProgrammerInfo(String proName,String proAddress,String mainSkill, int salary) {
	      //필드초기화...
	      this.proName = proName;
	      this.proAddress = proAddress;
	      this.mainSkill = mainSkill;
	      this.salary = salary;
	   }
	   public String getMainSkill() {
		   return mainSkill;
	   }

}
```
```java
ProgammerTest.java

package com.edu.cons.test;

import com.edu.cons.NoteBook;
import com.edu.cons.Programmer;

public class ProgrammerTest { //테스트클래스

	public static void main(String[] args) { //main메소드
		/*
		 * 1. Programmer 객체를 생성..이름을 james로
		 * 2. james가 삼성 노트북 한대를 구매함
		 * 3. james가 구매한 노트북의 정보를 
		 *    출력함
		 *    이때 james의 기술셋(mainSkill)도 함께 출력함
		 */
		Programmer james = new Programmer("James","NY","JAVA",300000);
		NoteBook nb = new NoteBook("SAMSUNG",200,1234);
		//james가 노트북을 구매...Has A Relation
		james.buyNoteBook(new NoteBook("SAMSUNG",200,1234));
		System.out.println("James의 주력 기술은"+james.getMainSkill()+"입니다.");
		//james가 구매한 노트북 정보를 출력... 반환된 노트북 출력
		james.getNoteBook().printInfo();
	}

}
```
```java
NoteBook noteBook;
 ```
Programmer클래스 안에서 NoteBook noteBook;필드를 선언한다.
```java
public void buyNoteBook(NoteBook noteBook) {
		   this.noteBook = noteBook;
	   }
public NoteBook getNoteBook() {
		   return noteBook;
	   }
```
Progammer에서 noteBook 필드변수에 대한 setter와 getter를 생성한다.
```java
Programmer james = new Programmer("James","NY","JAVA",300000);
NoteBook nb = new NoteBook("SAMSUNG",200,1234);
james.buyNoteBook(new NoteBook("SAMSUNG",200,1234));
james.getNoteBook().printInfo();
```
james가 노트북을 구매, james가 구매한 노트북정보를 출력

### Encapsulation(캡슐화)
1. 필드 앞에 private 지정 -- 다른 클래스에서 필드에 값 할당을 못한다.(직접적인 접근을 막는다)
2. void setXxx(0,0) / int getXxx( )는 public으로 지정한다.
   
   Field값은 set( ) / get( )으로 소통한다. public으로 열어둔다.
4. setXxx( )메소드에서 필드초기화 되기 직전에 받은 값이 타당한지에 대한 유효성 검사를 한다.
   
   set에 제어문을 넣어야한다.
   
### Array란?
같은 데이타 타입을 가지는 서로 다른 값들을 하나의 변수로 처리하는 것.

- Array 선언
1. 선언 ::  int[] arr;
2. 생성(반드시 사이즈를 명시) ::  arr = new int[3];
3. 초기화(새로운값 할당) ::  arr[0]=11; arr[1]=22; arr[2]=33;
4. 선언,생성,초기화 한번에 ::  int[] arr = {11,22,33};
5. Resizing이 안된다.
  한번만든 배열객체를 가지고 사이즈를 수정하게 되면 새로운 객체가 만들어진다. 
  처음만든 객체는 쓰레기객체가 된다.(참조가 끊어진다) 
6. 다른 사이즈를 가진 배열의 내용을 copy해올 수 있다 -> System.arrayCopy( )

### Access Modifier(접근지정자)
접근을 허용하는 범위를 키워드로 지정한것이다.
1. private : 같은 클래스에서만 접근을 허용한다.
2. default : 접근지정자로 지정안한다. 같은 폴더안에서만 접근을 허용한다.
3. protected : 같은 폴더안에서만 접근을 허용한다. 상속관계시 public과 동일한 접근범위이다.
4. public : 어디에서든 접근 가능하다.

### Method Overloading
1. 상속과 전혀 상관없이 하나의 클래스에서 일어나는 것이다.
2. 하는 일은 동일하지만 처리하는 데이타들을 달리할 때 사용한다.
3. 메소드이름은 반드시 동일해야한다.
4. 인자값은 반드시 달라야한다.
5. 리턴타입은 상관없다.

### 생성자 Overloading
1. 하나의 클래스안에서 생성자를 여러개 사용할 수 있다.
2. this( )와 함께 사용된된다.
3. 생성자이름이 같아야한다.
4. 인자값은 반드시 달라야한다.

### Method Overriding
1. 상속관계에 있는 2개의 클래스에서 작용하는 기능이다.
2. 부모의 성질을 모두 물려받고 자식에서 그것을 고친다.
3. 메소드 선언부는 모두 일치한다.(이름, 인자값, 리턴타입)
4. 메소드 구현부는 달라야한다.
5. 서로 다른 상속관계의 클래스에서 발생한다.

### Inheritance
```java
@Override
	public String getDetails() {//반환메소드
		return super.getDetails()+"subject :"+subject;
	}
	
	@Override
	public String toString() {
		return super.toString()+"subject :"+subject;
	}
```
```java
~Test
System.out.println(t.getDetails());
System.out.println(t);
```
toString을 사용하면 object메소드 생략가능하다.

### Polymorphism
1. 객체를 생성할때 부모타입으로 다양한 자식을 만들어야한다.
2. 상속이 전제가 된다.
3. 타입이 다른 이기종간의 서브클래스를 단일하게 핸들링하려면 한단계위인 슈퍼클래스에서 관리해야한다.
4. 부모타입의 클래스로 자식을 생성하는 것
5. 1) Virtual Method Invocation(가상함수호출) : 부모타입으로 자식객체를 생성하고 Overriding된 메소드를 부모타입의 변수로 호출하면 발생하는 원리이다.
	- Complie Type Method : 부모의 메소드가 호출됨.
	- Runtime Type Method : 자식의 메소드가 호출됨.
   2) object casting(형변환)
   
```java
  3 step......
 * public void addEmployee(Manager m){// }
 * public void addEmployee(Engineer eg){// }
 * public void addEmployee(Secretary sc){// }
 
 * 4 step...3단계와 같은 역할을 하지만 단 1번만 정의하면 된다.
 * public void add(Employee e){
 *   if(e instanceof Manager){ 
 *  }
 *  if(e instanceof Engineer){
 *  }
 *  if(e instanceof Secretary){
 *  }
 ```
 
### Static
1. static으로 지정된 멤버는 객체 생성할 필요없이 바로 접근해서 사용가능하다.
2. class(실행파일...byteCode)파일이 메모리(JVM)에 로더되는 과정에서 미리 메모리에 올라간다.
3. static으로 지정한 변수는 Local레벨에서 사용할 수 없다.
4. static으로 지정된 변수는 생성된 객체들에서 공유된다.
5. static키워드는 상수를 지정할때 쓰이는 final키워드와 거의 함께 많이 쓰인다.
6. final은 내가마지막이야라는 의미를 가지는 키워드이다.
7. final + 변수 : 상수값
8. final + 메소드 : 오버라이딩 금지
9. final + 클래스 : 상속금지
```java
static String name = "길똥이";//static V
	static int age = 19;//static V
	int count = 1;//field

	public static void getMember() {
		System.out.println("우/유/빛/깔/"+name);
	}
	
	//non-static
	public void getMember2() {
		//static String address = "한남동";
		System.out.println("우/유/빛/깔/"+name);
	}


public class StaticExamTest1 {

	public static void main(String[] args) {
		Member.getMember();//static
		
		Member m = new Member();//non-static
		m.getMember2();
	}
```
1. static으로 지정한 메소드는 객체 생성할 필요없이 클래스이름.메소드로 바로사용가능하다.
2. static영역에서는 non-static한 멤버를 사용할수 없기때문에 객체를 생성해서 사용해야한다.


### Singleton Pattern
1. 하나의 클래스로부터 오직 하나의 객체만을 생성하는 패턴이다.
2. private static으로 해당 클래스에서 객체를 일단 하나는 생성한다.
3. 다른곳에서 객체생성을 못하도록 생성자앞에 private를 붙인다.
4. 하나 만들어놓은 객체를 여기저기서 가져다 쓸 수있도록 public으로 리턴하는 기능을 만든다.
```java
class Factory{
	private static Factory factory = new Factory(); //1
	private Factory(){ //2
		System.out.println("Factory Only One Creating....");
	}
	public static Factory getInstance() {//3
		return factory;
	}
}
public class StaticExamTest5 {
	public static void main(String[] args) {
		System.out.println("Singleton Pattern....");
		
		//Factory factory1 = new Factory(); private으로 막혀있어 객체생성안된다.
		Factory factory1 = Factory.getInstance();
		Factory factory2 = Factory.getInstance();
		Factory factory3 = Factory.getInstance();
		
		System.out.println(factory1);
		System.out.println(factory2);
		System.out.println(factory3);
		
	}

}
```
1. 만들어진것을 받아서 사용해야함 - getInstance()호출
2. 메모리에 올려야하는데 객체생성을 못함.
3. static으로 미리 메모리에 올려둬서 사용해야함.
4. getInstance()를 여러번 호출해서 Factory객체를 여러번 리턴받았다.
5. 이때 factory1,factory2,factory3가 서로 다른 객체가 아닌지 어떻게 확인?...주소값으로 확인한다.		
### Interface
1. 인터페이스는 구현부가 없는 기능의 Template(추상적인기능)들 만으로 구성된다.
2. 구현부가 없는 메소드가 추상메소드이다.
3. 인터페이스의 구성요소는 Template기능(추상메소드), public static final 상수이다.
4. 인터페이스안에서는 무조건 변수앞에 public static final을 붙여야한다.
5. 구현부가 없는 메소드 선언일때는 abstract키워드를 붙여야한다.

```java
public interface Flyer {
	public static final int SPEED = 100; 
	
	public abstract void fly();
	 public abstract void land();
	 public abstract void take_off();
}
```
```java
public class Bird implements Flyer{

	//구현부가 없는데 구현부를 만듬 :: 오버라이딩임.
	@Override
	public void fly() {
		System.out.println("Bird fly...");
	}

	@Override
	public void land() {
		System.out.println("Bird land...");
	}

	@Override
	public void take_off() {
		System.out.println("Bird take_off...");		
	}
	
	//Bird만의 기능
	public String layEggs() {
		return "알을 낳다";
	}
	public String buildNest() {
		return "둥지를 짓다";
	}

}
```
인터페이스를 상속받는 클래스는 반드시 인터페이스의 추상메소드를 구현해야한다.
```java
public class FlyerTest1 {

	public static void main(String[] args) {
		//완벽한 미완성이기때문에 객체생성을 할 수 없다.
		//Flyer f1 = new Flyer();
	
		Flyer bird  = new Bird();
		Flyer airplane = new AirPlane();
		Flyer superman = new SuperMan();
		
		Flyer[] flyers = {
				bird,airplane,superman
		};
		
		for(Flyer f : flyers) {
			if(f instanceof Bird) {
				System.out.println(((Bird) f).layEggs());
				f.fly();
				f.land();
				System.out.println("----------------------");
			}
```
인터페이스는 객체생성의 대상이 될수 없지만 type으로서는 존재한다.












