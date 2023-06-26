# Model, ModelAndView 차이

### 요즘은 잘 사용하진 않는다.
  - @Controller 어노테이션 사용하기 전부터 사용되었고, Spring MVC가 @Controller 어노테이션을 지원하기 시작한 후로
  - ModelAndView를 잘 사용하지 않는다고 한다.
  - 또한 스택오버플로우에서도 ModelAndView를 직접 반환하는건 구식이라고 말함. 
  - (https://stackoverflow.com/questions/7383622/spring-mvc-controllers-return-type)


### ModelAndView 예제
- Model값을 넣을떄 addAttribute() 사용
```java
@Controller
@RequestMapping("/main")
public class BoardController {

    @RequestMapping(value = "/")
    public ModelAndView index() {
        ModelAndView mav = new ModelAndView();
        mav.addObject("name", "홍길동");
        mav.setViewName("main/index");

        return mav;
    }

    @RequestMapping(value = "/")
    public ModelAndView index() {
        ModelAndView mav = new ModelAndView();

        List<BoardDto> lists = boardService.getLists(start, end, searchKey, searchValue);
        mav.addObject("lists", list);
        mav.setViewName("main/index");

        return mav;
    }
}
```

### Model 예제
- Model + View를 합쳐놓은 방식
- 값을 넣을때는 addObject()를 사용, 값을 보낼때는 View를 세팅하것은 setViewName()을 사용
```java
@Controller
@RequestMapping("/main")
public class BoardController {

    @RequestMapping(value = "/")
    public String index(Model model) {
        model.addAttribute("name", "홍길동");

        return model;
    }

    @RequestMapping(value = "/")
    public String index(Model model) {
        model.addAttribute("lists", boardService.getLists(start, end, searchKey, searchValue));
        return "main/index";
    }
```
