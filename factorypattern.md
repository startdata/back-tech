## 팩토리 패턴

> 객체 생성부분을 따로 추상화한 패턴  
> 상속 관계에 있는 두 클래스에서 상위 클래스가 뼈대를 결정  
> 하위 클래스에서 객체 생성에 관현 내용 결정

### 장점

- 상위 클래스와 하위 클래스가 분리되기 때문에
  - 느슨한 결합을 가지며
  - 상위 클래스에서 객체 생성에 관여하지 않기 때문에 더 유연함
  - 객체 생성 로직이 따로 있기 때문에 리팩터링한다면 한 곳만 고칠 수 있게 된다.
    > ex. 레시피라는 구체적인 내용(하위 클래스)를 컨베이어 벨트를 통해 전달, 바리스타 공장(상위 클래스)에서 레시피를 토대로 생산

```ts
const num = new Object(20);
const str = new Object("abc");
num.constructor.name; // number
str / constructor.name; // String
```

> 전달받은 값에 따라 다른 객체를 생성하고, 인스턴스의 타입을 정한다.

```ts
class Latte {
  constructor() {
    this.name = "latte";
  }
}

class Espresso {
  constructor() {
    this.name = "Espresso";
  }
}

class LatteFactory {
  static createCoffee() {
    return new Latte();
  }
}

class EspressoFactory {
  static createCoffee() {
    return new Espresso();
  }
}

const factoryList = { LatteFactory, EspressoFactory };

class CoffeeFactory {
  static createCoffee(type) {
    const factory = factoryList[type];
    return factory.createCoffee();
  }
}

const main = () => {
  // 라떼 주문
  const coffee = CoffeeFactory.createCoffee("LatteFactory");
  // 커피 이름
  console.log(coffee.name); // latte
};
main();
```

> CoffeeFactory에서 LatteFactory의 인스턴스를 생성하는 것이 아니라 LatteFactory에서 생성한 인스턴스를 CoffeeFactory에 주입하고 있기 때문에  
> 의존성 주입이라고도 할수 있다.
