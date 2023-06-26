# @Controller, @Requestmapping


### @Controller
- 내부에 @Component 어노테이션이 존재해 컴포넌트 스캔의 대상
- 스프링이 자동으로 스프링 빈으로 등록
- 스프링 MVC에서 어노테이션 기반 컨트롤러로 인식하게 함

### @RequstMapping
- 요청 정보를 매핑
- 해당 url이 호출되면 해당 메서드가 호출
- 어노테이션 기반 동작이기 떄문에 메서드 이름은 자유


### 예시
```java
package com.mycompany.view.address;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

import com.mycompany.biz.address.AddressVO;
import com.mycompany.biz.address.Impl.AddressDAO;

@Controller
public class AddressController {
	
	@RequestMapping(value = "/insertAddress.do")
	public String insertAddress(AddressVO vo, AddressDAO addressDAO) {
		addressDAO.insertAddress(vo);
		return "getAddressList.do";
	} 
	
	@RequestMapping("/updateAddress.do")
	public String updateAddress(AddressVO vo, AddressDAO addressDAO) {
		addressDAO.updateAddress(vo);
		return "getAddressList.do";
	}
	
	@RequestMapping("/deleteAddress.do")
	public String deleteAddress(AddressVO vo, AddressDAO addressDAO) {
		addressDAO.deleteAddress(vo);
		return "getAddressList.do";
	}
	
	@RequestMapping("/getAddress.do")
	public String getAddress(AddressVO vo, AddressDAO addressDAO, Model model) {
		model.addAttribute("address", addressDAO.getAddress(vo)); // 세션 등록됨 ModelANdView는 addObject()
		return "addressbook_edit_form.jsp";
	}
	
	@RequestMapping("/getAddressList.do")
	public String getBoardList(AddressVO vo, AddressDAO addressDAO, Model model) {
		model.addAttribute("addressList", addressDAO.getAddressList(vo));
		return "addressbook_list.jsp";
	}
	
}
```
