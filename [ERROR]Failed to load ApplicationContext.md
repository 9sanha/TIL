#### [ERROR]

##### error 내용

``` markdown
Failed to load ApplicationContext
java.lang.IllegalStateException: Failed to load ApplicationContext
```

<img src="https://images.velog.io/images/9sanha/post/1b3c617b-c205-4b3d-a87c-65e346ca1d69/image.png" style="zoom: 80%;" />

##### error 발생 원인과 해결 (산피셜)

- 오류내용을 보면 `ApplicationContext`을 로드할 수 없다고 나온다.
- 코드 상에 ApplicationContext을 쓰는 코드가 있는데, 그 코드에는 @autowired 어노테이션이 붙어있다. 
  (@autowired - 스프링이 IoC 컨테이너에서 상황에 맞게 Bean을 자동으로 주입. 단어 그대로 자동 연걸!)
- 즉 ApplicationContext를 쓰려면 스프링 컨테이너를 사용해야한다

``` java
// MVC TEST 클래스 상단에 추가
@MockBean(JpaMetamodelMappingContext.class)
```



- 스프링의 컨테이너를 사용하지 않으면 mock을 써도 무관하지만 스프링의 컨테이너를 쓰려면 mockBean 어노테이션을 꼭 사용해야한다.
- mock과는 다르게 mockBean은 Spring framework(org.springframework.boot.test.mock.mockito) 내에 있기 때문에 스프링 영역의 컨테이너에 객체를 등록해준다! (MockBean은 Spring context 영역)
- 때문에 Autowired가 정상 작동하여 test 코드를 실행했을 때 ApplicationContext를 정상적으로 로드해준다.

##### 참고사이트 

- https://blusky10.tistory.com/330
- https://gunju-ko.github.io/toby-spring/2019/03/25/IoC-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%99%80-DI.html
- https://1-7171771.tistory.com/136
- https://stackoverflow.com/questions/53524827/springboot-webmvctest-and-mockbean-not-working-as-expected
- https://pythonq.com/so/java/881630
