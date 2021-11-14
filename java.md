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
















