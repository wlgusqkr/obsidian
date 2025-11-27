
##### AllArgsConstructor를 지양하는 이유
- AllArgsConstructor는 클래스 선언 순서대로 생성자를 만들어서 만약 
```
public Person {
	private String name;
	private String alias;
}
// 이런 코드가 있다면 
Person jihyeon = new Person("박박지현", "박지현");
// 이렇게 썼을 때 이름과 별명이 반대로 들어갈 수 있다.
// 빌더 패턴을 쓰기로 약속하고 사용하면 괜찮을 수 있지만 
// 규모가 커지면 이런 사소한 오류가 엄청난 오류를 불러올 수도..
```
#### 결론
1. @AllArgsConstructor와 @Builder를 동시에 쓰고 빌더패턴으로만 만들기로 약속하기
2. Builder를 생성자 위에 붙이기 
3. @AllArgsConstructor(access = AccessLevel.PRIVATE)와 @Builder로 하면 보통 객체에서는 new 로 객체 생성을 막고 빌더로만 생성을 유도할 수 있다. 그러나 Lombok이 만들어주는 생성자는 단순히 값만 대입하기 때문에 검증 로직이 필요하다면 생성자 위에 Builder를 붙여서 사용해야한다.

#### 추가
@RequiredArgsConstructor도 동일하다.
하지만 Bean을 자동 주입해주는 건 스프링에서 알맞은 타입+이름을 보고 빈을 넣어준다.

참고 : 
https://velog.io/@skb0516/AllArgsConstructor%EB%A5%BC-%EC%A7%80%EC%96%91%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-Builder%EC%99%80-%ED%95%A8%EA%BB%98-%EC%93%B8-%EB%95%8C