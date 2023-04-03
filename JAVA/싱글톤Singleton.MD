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
