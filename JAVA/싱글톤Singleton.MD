# 싱글톤

### 생성(Creational) 패턴 중 하나로써 객체를 오직 하나만 생성하여 생성된 객체를 프로그램 어디에서나 접근하여 사용할 수 있도록 하는 패턴
- 간단하게 애플리케이션 전체에서 단 하나의 객체만 생성하고 필요할 때마다 이 객체에 접근하여 사용하겠다는 의미

## static
- 간단하게 자바에서는 static 키워드를 사용하면 메모리에 한번 할당되어 프로그램이 종료될 때 해제 된다
- 따라서 static을 통해 객체를 생면하면 프로그램이 종료되기 전까지 계속해서 메모리에 남아있기 때문에 다른 곳에서 똑같은 객체에 접근할 수 있도록 해줌

## 예제

- 회사 이름, 주소를 가져오는 싱글톤 예제
~~~java
// getter setter는 cmd n 사용하기(편함)
public class CompanyInfo {
    private static CompanyInfo instance;

    private String companyName;
    private String companyAddr;

    private CompanyInfo() {

    }

    public static CompanyInfo getInstance() {
        if (instance == null) {
            synchronized(CompanyInfo.class) {
                instance = new CompanyInfo();
            }
        }
        return instance;
    }

    public String getCompanyName() {
        return companyName;
    }

    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }

    public String getCompanyAddr() {
        return companyAddr;
    }

    public void setCompanyAddr(String companyAddr) {
        this.companyAddr = companyAddr;
    }


}
~~~

#### Test1
~~~java
public class TestClass1 {

    public static void main(String[] args) {
        CompanyInfo companyInfo = CompanyInfo.getInstance();

        // setter 접근
        companyInfo.setCompanyName("삼성");
        companyInfo.setCompanyAddr("서울");

        System.out.println("회사의 이름은 " + companyInfo.getCompanyName());
    }
}
~~~

#### Test2
~~~java
public class TestClass2 {

    public static void main(String[] args) {
        CompanyInfo companyInfo2 = CompanyInfo.getInstance();

        companyInfo2.setCompanyName("엘지");
        companyInfo2.setCompanyAddr("경기");

        System.out.println("회사의 이름은 : " + companyInfo2.getCompanyName());
        System.out.println("회사의 주소는 : " + companyInfo2.getCompanyAddr());
    }
}
~~~

------------------------------------------------------------------------

## 예제2 ( 정수기 물 사용 )
~~~java
public class WaterPurifier {
    // private 선언 외부 접근x
    // 다만, 접근할땐 동일한 객체를 위해 static으로 선언
    private static WaterPurifier waterPurifier;

    private int amount;

    // private으로 선언하여 외부에서 접근 x
    private WaterPurifier() { setAmount(100); }

    public static WaterPurifier getInstance() {
        // 초기 호출 시 waterPurifier 객체 생성
        if(waterPurifier == null) {
            waterPurifier = new WaterPurifier();
        }
        return waterPurifier;
    }

    public int getAmount() {
        return amount;
    }

    public void setAmount(int amount) {
        this.amount = amount;
    }

    public void useWaterPurifier() {
        amount--;
    }

    public int remainAmount() {
        return 100 - amount;
    }
}
~~~

~~~java
public class WaterPurifierPRac {
    public static void main(String[] args) {
        WaterPurifier waterPurifier1 = WaterPurifier.getInstance();

        waterPurifier1.useWaterPurifier();
        waterPurifier1.useWaterPurifier();

        int in = waterPurifier1.remainAmount();


        System.out.println("정수기가 100에서 " + in + "만큼 사용했기에 " + waterPurifier1.getAmount() + " 남았습니다.");
    }
~~~

------------------------------------------------------------------------
출처

https://itstudy402.tistory.com/8

https://sorjfkrh5078.tistory.com/108



# 싱글톤
- 코드로 봐보기

~~~java
package step4_싱글톤;

// 싱글톤
class Company {
	
	private static Company instance = new Company(); // new Company(); 없으면 안되는건가??
	
	private Company() {} // getInstance만 불러오게 막아버림 private 걸어서
	
	
	public static Company getInstance() {
		if (instance == null) {
			instance = new Company();
		}
		return instance;
	}
	
}


public class CompanyEx {
	public static void main(String[] args) {
//		Company instance = new Company();
		
		Company c1 = Company.getInstance();
		Company c2 = Company.getInstance();
		Company c3 = Company.getInstance();
		
		System.out.println(c1); // 같은
		System.out.println(c2); // 주소에
		System.out.println(c3); // 있다
		
	}
}
~~~
