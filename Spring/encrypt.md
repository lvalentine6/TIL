암호화
=========

- 암호화 : 내가 원하는 대상들만 이해할 수 있도록 값을 변조시키는 것
- 복호화 : 변조된 값을 해석할수 있게 값을 변화 시키는것

암호화의 종류
=========

- 단방향 암호화 : 암호화만 가능하고 복호화는 불가능한 방식
- 양방향 암호화 : 암호화도 가능하고 복호화도 가능한 방식

카이사르 암호화
-----------

- 카이사르 암호화는 로마의 정치가이자 군인이었던 카이사르의 이름에서 기원하였다.
- 각각의 알파벳을 + 혹은 - 를 수행하여 암호화를 수행한다.

***

	@Test
	public void test2() {
		String text = "hello";
		
		StringBuffer encrypt = new StringBuffer();
		for(int i=0; i < text.length(); i++) {
			char c = text.charAt(i);
			c -= 5;
			encrypt.append(c);
		}
		log.debug("encrypt = {}", encrypt.toString());
		
		StringBuffer decrypt = new StringBuffer();
		for(int i=0; i < encrypt.length(); i++) {
			char c = encrypt.charAt(i);
			c += 5;
			decrypt.append(c);
		}
		log.debug("decrypt = {}", decrypt.toString());

***

이와 같이 C의 값을 조정하여 암호화를 수행하며 C의 값을 알면 복호화도 수행할 수 있다.


비트 연산자
-----------

비트연산자란 비트 단위의 논리 연산을 할 때 사용한다.

- & : 대응되는 비트가 모두 1이면 1을 반환한다. (AND 연산)
- ! : 대응되는 비트 중에서 하나라도 1이면 1을 반환함(OR 연산)
- ^ : 대응되는 비트가 서로 다르면 1을 반환함 (XOR 연산)
- ~ : 비트가 1이면 0으로 0이면 1로 반전시킴 (NOT 연산)
- << : 지정한 수만큼 비트들을 전부 왼쪽으로 이동시킴 (Left shift 연산)
- > > : 부호를 유지하면서 지정한 수만큼 비트를 전부 오른쪽으로 이동시킴 (Right shift 연산)

XOR 암호화
-----------

- 비트 연산자를 이용하여 암호화를 수행한다.
- spring-security-core 라이브러리를 사용하여 암호화, 복호화를 실행한다.

***

@Test
public void test() {
String origin = "hello";
log.debug("origin = {}", origin);

		PasswordEncoder encoder = new BCryptPasswordEncoder();
		String encrypt = encoder.encode(origin);
		log.debug("encrypt = {}", encrypt);
		
		boolean match = encoder.matches("hello", encrypt);
		log.debug("match = {}", match);
	}

***

도구
-----------

- PasswordEncoder
    - StandardPasswordEncoder
    - ScryptPasswordEncoder
    - BcryptPasswordEncoder
