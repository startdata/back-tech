# DI, IoC

## IoC

### IoC 란?

제어의 역전이라고 표현 하며, 메소드나 객체의 호출작업을 외부에서 결정해서 주입하는것

spring, nestjs 등의 프레임워크 에서 코드를 제어
코드를 작성하는 사람이 제어하는 것이 아니라 프레임워크에서 제어해서 제어의 역전

개발자는 부품을 개발하고 부품들을 조립하는 방식으로 개발

---

## DI

부품의 조립
부품들을 따로 만들어서 가져와서 조립해서 쓰자(ex.레고)

### DI란?

의존성 주입
부품(객체)를 직접생성하거나 제어 하지 않고
특정 부품에 필요한 부품을 외부에서 결정해서 연결(조립)시키는 것
