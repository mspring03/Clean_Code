# [02장] 의미 있는 이름

## 목차

  1. [들어가면서](#들어가면서)
  2. [의도를 분명히 밝혀라](#의도를-분명히-밝혀라)
  3. [그릇된 정보를 피하라](#그릇된-정보를-피하라)
  4. [의미 있게 구분하라](#의미-있게-구분하라)
  5. [발음하기 쉬운 이름을 사용하라](#발음하기-쉬운-이름을-사용하라)
  6. [검색하기 쉬운 이름을 사용하라](#검색하기-쉬운-이름을-사용하라)
  7. [인코딩을 피하라](#인코딩을-피하라)   
  7.1 [헝가리릭 표기법](#헝가리식-표기법)   
  7.2 [멤버 변수 접두어](#멤버-변수-접두어)   
  7.3 [인터페이스 클래스와 구현 클래스](#인터페이스-클래스와-구현-클래스)   
  8. [자신의 기억력을 자랑하지 마라](#자신의-기억력을-자랑하지-마라)
  9. [클래스 이름](#클래스-이름)
  10. [메서드 이름](#메서드-이름)
  11. [기발한 이름은 피하라](#기발한-이름은-피하라)
  12. [한 개념에 한 단어를 사용하라](#한-개념에-한-단어를-사용하라)
  13. [말장난을 하지 마라](#말장난을-하지-마라)
  14. [해법 영역에서 가져온 이름을 사용하라](#해법-영역에서-가져온-이름을-사용하라)
  15. [문제 영역에서 가져온 이름을 사용하라](#문제-영역에서-가져온-이름을-사용하라)
  16. [의미 있는 맥락을 추가하라](#의미-있는-맥락을-추가하라)
  17. [불필요한 맥락을 없애라](#불필요한-맥락을-없애라)
  18. [마치면서](#마치면서)

**[⬆ 위로가기](#목차)**
## 들어가면서
소프트웨어에서 이름은 어디나 쓰인다. 이렇듯 많이 사용하므로 이름을 잘 지으면 여러모로 편하다.   
 이 장에서는 이름을 잘 짓는 간단한 규칙을 몇가지 소개한다.

**[⬆ 위로가기](#목차)**
## 의도를 분명히 밝혀라
"의도가 분명하게 이름을 지으라"고 말하기는 쉽다. 여기서는 의도가 분명한 이름이 **정말로** 중요하다는 사실을 거듭 강조한다. 좋은 이름을 지으려면 시간이 걸리지만 좋은 이름으로 절약하는 시간이 훨씬 더 많다. 그러므로 이름을 주의깊게 살펴 더 나은 이름이 떠오르면 개선하기 바란다.   

변수나 함수, 클래스 이름은 다음과 같은 질문에 모두 답해야 한다. 존재 이유는? 수행 기능은? 사용 방법은?   
따로 **주석이 필요하다면** 의도를 분명히 드러내지 못했다는 말이다.   

```typescript
let d: number; // 경과 시간(단위: 날짜)
```

이름 d는 아무 의미도 드러나지 않는다. 경과 시간이나 날짜라는 느낌이 안 든다. 측정하려는 값과 단위를 표현하는 이름이 필요하다.
```typescript
let elapsedTimeInDays: number;
let daysSinceCreation: number;
let daysSinceModification: number;
let fileAgeInDays: number;
```

의도가 드러나는 이름을 사용하면 코드 이해와 변경이 쉬워진다. 다음 코드는 무엇을 할까?
```typescript
function getThem(): Array<number[]> {
    let list1: Array<number[]> = new Array<number[]>();
    for (let x of theList)
        if (x[0] === 4)
            list1.push(x);
    return list1;
}
```

코드가 하는 일을 짐작하기 어렵다. 왜일까? 복잡한 문장은 없다. 공백과 들여쓰기도 적당하고 변수 상수의 개수도 적당하다.  
문제는 코드의 단순성이 아니라 코드의 함축성이다. 다시 말해, 코드의 맥락이 코드 자체에 명시적으로 드러나지 않는다. 위 코드는 암암리에 독자가 다음과 같은 정보를 안다고 가정한다.

    1. theList에 무엇이 들었는가?
    2. theList에서 0번째 값이 어째서 중요한가?
    3. 값 4는 무슨 의미인가?
    4. 함수가 반환하는 리스트 list1을 어떻게 사용하는가?
위 코드엔 이와 같은 정보가 드러나지 않는다. 하지만 정보 제공은 **충분히 가능했었다.**   
지뢰찾기 게임을 만든다고 가정하면 theList가 게임판이라는 사실을 안다.    
게임판에서 각 칸은 단순 배열로 표현한다. 배열에서 0번째 값은 칸 상태를 뜻한다. 값 4는 깃발이 꽂힌 상태를 가리킨다. 각 개념에 이름만 붙여도 코드가 상당히 나아진다.

```typescript
function getFlaggedCells(): Array<number[]> {
    let flaggedCells: Array<number[]> = new Array<number[]>();
    for (let cell of gameBoard)
        if (cell[STATUS_VALUE] === FLAGGED)
            flaggedCells.push(cell);
    return flaggedCells;
}
```

위에서 보듯, 코드의 단순성은 변하지 않았다. 연산자 수와 상수 수는 앞의 예제와 똑같고 들여쓰기 단계도 동일하다. 그런데도 코드는 더욱 명확해졌다.   
한 걸음 더 나아가, number배열을 사용하는 대신, 칸을 간단한 클래스로 만들어도 되겠다. isFlagged라는 좀 더 명시적인 함수를 사용해 FLAGGED라는 상수를 감춰도 좋겠다. 새롭게 개선한 결과는 다음과 같다.

```typescript
function getFlaggedCells(): Array<Cell> {
    let flaggedCells: Array<Cell> = new Array<Cell>();
    for (let cell of gameBoard)
        if (cell.isFlagged())
            flaggedCells.push(cell);
    return flaggedCells;
}
```

단순히 이름만 고쳤는데도 함수가 하는 일을 이해하기 쉬워졌다. 바로 이것이 **좋은 이름이 주는 위력이다.**

**[⬆ 위로가기](#목차)**
## 그릇된 정보를 피하라
프로그래머는 코드에 그릇된 단서를 남겨서는 안 된다. 그릇된 단서는 코드의 의미를 흐린다. 나름대로 **널리 쓰이는 의미가 있는 단어**를 다른 의미로 사용해도 안된다.   

여러 계정을 그룹으로 묶을 때, 실제 List가 아니라면, accountList라 명명하지 않는다. 프로그래머에게 **List라는 단어는 특수한 의미다**. 그러므로 accountGroup, bunchOfAccounts, 아니면 단순히 Accounts라 명명한다.   

**서로 흡사한 이름**을 사용하지 않도록 주의한다.   

유사한 개념은 유사한 표기법을 사용한다. 이것도 **정보**다. 일관성이 떨어지는 표기법은 그릇된 정보다.   

이름으로 그릇된 정보를 제공하는 진짜 끔찍한 예가 소문자 L이나 대문자 O변수다. 소문자 L은 숫자 1처럼 보이고 대문자 O는 숫자 0처럼 보인다. 어떤 경우는 코드 작성자가 글꼴을 바꿔 차이를 드러내는 해결책을 제안했다. 이것은 문서나 구전으로 미래 개발자 모두에게 알려야 하는 해결책이다. **이름만 바꾸면** 문제가 깨끗이 풀리는데 괜스레 일거리를 만들 필요 없다.


**[⬆ 위로가기](#목차)**
## 의미 있게 구분하라
컴파일러나 인터프리터만 통과하려는 생각으로 코드를 구현하는 프로그래머는 스스로 문제를 일으킨다. 예를 들어, 동일한 범위 안에서는 다른 두 개념에 같은 이름을 사용하지 못한다.   
 
컴파일러를 통과할지라도 연속된 숫자를 덧붙이거나 불용어를 추가하는 방식은 적절하지 못한다. 이름이 달라야 한다면 의미도 달라져야 한다.
```typescript
function copyStrings(a1: string[], a2: string[]): void {
    for (let i = 0; i < a1.length; i++) {
        a2[i] = a1[i];
    }
}
```

함수 인수 이름으로 source와 destination을 사용한다면 코드 읽기가 훨씬 더 쉬워진다.   

불용어를 추가한 이름 역시 아무런 정보도 제공하지 못한다. Produce, ProdductInfo, ProduceData라는 클래스처럼 개념을 구분하지 않은 채 이름만 달리한 경우다. Info나 Data는 a, an, the와 마찬가지로 의미가 **불분명한 불용어다.**   

명확한 관례가 없다면 변수 moneyAmount는 money와, customerInfo는 customer와, accountData는 account와, theMessage는 message와 구분이 안 된다. **읽는 사람이 차이를 알도록** 이름을 지어라.

**[⬆ 위로가기](#목차)**
## 발음하기 쉬운 이름을 사용하라
사람들은 **단어에 능숙**하다. 우리 두뇌에서 상당 부분은 단어라는 개념만 전적으로 처리한다. 그러므로 **발음하기 쉬운 이름을 선택한다.**   
발음하기 어려운 이름은 토론하기도 어렵다. 바보처럼 들리기 십상이다. "흠, 여기 비 씨 알 3 씨 엔 티에 피 에스 지큐가 있군요. 보입니까? **발음하기 쉬운 이름**은 중요하다. 프르그래밍은 **사회 활동**이기 때문이다.   
다음 두 예제를 비교해보자.
```typescript
class DtaRcrd102 {
    private genymdhms: Date;
    private modymdhms: Date;
    private pszgint: string = '102';
}

class Customer {
    private generationtimestamp: Date;
    private modification: Date;
    private recordId: string = '102';
}
```

둘째 코드는 지적인 대화가 가능해진다. "마이키, 이 레코드 좀 보세요. 'Generation Timestamp'값이 내일 날짜입니다! 어떻게 이렇죠?

**[⬆ 위로가기](#목차)**
## 검색하기 쉬운 이름을 사용하라
문자 하나를 사용하는 이름과 상수는 텍스트 코드에서 쉽게 **눈에 띄지 않는다**는 문제점이 있다.   
개인적으로 간단한 메서드에서 로컬 변수만 한 문자를 사용한다. **이름 길이는 범위 크기에 비례해야 한다.** 변수나 상수를 코드 여러 곳에서 사용한다면 **검색하기 쉬운 이름**이 바람직하다. 다음 두 예제를 비교해보자.
```typescript
for (let j = 0; j < 34; j++) {
    s += (t[j] * 4) / 5;
}

와

let realDaysPerIdealDay: number = 4;
const WORK_DAYS_PER_WEEK: number = 5;
let sum: number = 0;
for (let j = 0; j < NUMBER_OF_TASKS; j++) {
    let realTaskDays: number = taskEstimate[j] * realDaysPerIdealDay;
    let realTaskWeeks: number = (realTaskDays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

위 코드에서 sum이 별로 유용하진 않으나 최소한 검색이 가능하다. **이름을 의미있게 지으면 함수가 길어진다.**

**[⬆ 위로가기](#목차)**
## 인코딩을 피하라
굳이 부담을 더하지 않아도 이름에 **인코딩할 정보는 아주 많다.** 유형이나 범위정보까지 인코딩에 넣으면 그만큼 이름을 해독하기가 어려워진다. 인코딩한 이름은 거의가 발음하기 어려우며 오타가 생기기도 쉽다.

**[⬆ 위로가기](#목차)**
> ### 헝가리식 표기법
이름 길이가 제한된 언어를 사용하던 옛날에는 어쩔 수 없이 안타까워하면서도 이 규칙을 위반했다. 포트란은 첫 글자로 유형을 표현했다. 초창기 베이식은 글자 하나에 숫자 하나만 허용했다.   
당시는 컴파일러가 타입을 점검하지 않았으므로 프로그래머에게 타입을 기억할 단서가 필요했다.   

이제는 헝가리식 표기법이나 기타 인코딩 방식이 오히려 방해가 될 뿐이다. 변수, 함수, 클래스 이름이나 타입을 바꾸기가 어려워지며, 읽기도 어려워진다. 독자를 오도할 가능성도 커진다.   
```typescript
let phoneString: PhoneNumber;
// 타입이 바뀌어도 이름은 바뀌지 않는다!
```

**[⬆ 위로가기](#목차)**
> ### 멤버 변수 접두어
이제는 멤버 변수에 m_이라는 접두어를 붙일 필요도 없다. 클래스와 함수는 접두어가 필요없을 정도로 작아야 마땅하다.
```typescript
class Part {
    private m_dsc: string;  // 설명 문자열
    setName(name: string) {
        this.m_dsc = name;
    }
}

_____________________________________________________

class Part {
    private description: string;
    setDescription(description: string) {
        this.description = description;
    }
}
```

게다가 사람들은 접두어 또는 접미어를 무시하고 이름을 해독하는 방식을 재빨리 익힌다. 코드를 읽을수록 접두어는 관심 밖으로 밀려난다. 결국은 접두어는 옛날에 작성한 구닥다리 코드라는 징표가 되버린다.

**[⬆ 위로가기](#목차)**
> ### 인터페이스 클래스와 구현 클래스
때로는 인코딩이 필요한 경우도 있다. 예를 들어, 도형을 생성하는 ABSTRACT FACTORY를 구현한다고 가정하자. 이 팩토리는 인터페이스 클래스이고 구현은 구체 클래스에서 한다. 그렇다면 두 클래스 이름을 어떻게 지어야 좋을까? IShaepFactory와 ShapeFActory? 옛날 코드에서 많이 사용하는 접두어 I는 잘해봤자 주의를 흐트리고 나쁘게는 과도한 정보를 제공한다.

내가 다루는 클래스가 인터페이스라는 사실을 남에게 알리고 싶지 않다. 그래서 인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩해야 한다면 **구현 클래스 이름**을 택하겠다. ShapeFactoryImp 나 심지어 CShapeFactory가 IShapeFactory보다 좋다.


**[⬆ 위로가기](#목차)**
## 자신의 기억력을 자랑하지 마라
독자가 코드를 읽으면서 변수 이름을 자신이 아는 이름으로 변환해야 한다면 그 변수 이름은 바람직하지 못하다. 이는 일방적으로 문제 영역이나 해법 영역에서 사용하지 않는 이름을 선택했기 때문에 생기는 문제다.   
문자 하나만 사용하는 변수 이름은 문제가 있다. 루프에서 반복 횟수를 세는 변수 i, j, k는 괜찮다.   

똑똑한 프로그래머와 전문가 프로그래머의 차이점을 하나 들자면, 전문가 프로그래머는 **명료함이 최고**라는 사실을 이해한다. 전문가 프로그래머는 자신의 능력을 좋은 방향으로 사용해 남들이 이해하는 코드를 내놓는다.


**[⬆ 위로가기](#목차)**
## 클래스 이름
클래스 이름과 객체 이름은 **명사나 명사구**가 적합하다. Customer, WikiPage, Account, AddressParser 등이 좋은 예다. Manager, Processor, Data, Info 등과 같은 단어는 피하고, **동사는 사용하지 않는다.**

**[⬆ 위로가기](#목차)**
## 메서드 이름
메서드 이름은 **동사나 동사구**가 적합하다. postPayment, deletePage, save 등이 좋은 예다. 접근자, 변경자, 조건자는 값 앞에 get, set, is를 붙인다.

```typescript
let name: string = employee.getName();
customer.setName('mike');
if (paycheck.isPosted()) { ... }
```

생성자를 중복정의 할 때는 **정적 팩토리 메서드**를 사용한다. 메서드는 인수를 설명하는 이름을 사용한다. 예를 들어, 다음 두 예제를 살펴보자.

```typescript
let fulcurmPoint: Complex = Complex.FromRealNumber(23.0);

// 위 코드가 아래 코드보다 좋다.

let fulcrumPoint: Complex = new Complex(23.0);
```

생성자 사용을 제한하려면 해당 생성자를 private로 선언한다.

**[⬆ 위로가기](#목차)**
## 기발한 이름은 피하라
이름이 너무 기발하면 저자와 유머 감각이 비슷한 사람만, 그리고 농담을 기억하는 동안만, 이름을 기억한다.    
**재미난 이름보다 명료한 이름**을 선택하라. 의도를 분명하고 솔직하게 표현하라.


**[⬆ 위로가기](#목차)**
## 한 개념에 한 단어를 사용하라
추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다. 예를 들어, 똑같은 메서드를 클래스마드 fetch, retieve, get으로 제각각 부르면 혼란스럽다. 따라서 메서드 이름은 **독자적이고 일관적**이어야 한다.

이름이 다르면 독자는 당연히 클래스도 다르고 타입도 다르리라 생각한다. **일관성 있는 어휘**는 코드를 사용할 프로그래머가 반갑게 여길 선물이다.


**[⬆ 위로가기](#목차)**
## 말장난을 하지 마라
한 단어를 두 가지 목적으로 사용하지 마라. 다른 개념에 같은 단어를 사용한다면 그것은 **말장난**에 불과하다.   
"한 개념에 한 단어를 사용하라"는 규칙을 따랐더니, 예를 들어 여러 클래스에 add라는 메서드가 생겼다. 모든 add 메서드의 매개변수와 반환값이 의미적을 똑같다면 문제가 없다.   

하지만 때로는 프로그래머가 같은 맥락이 아닌데도 '일관성'을 고려해 add라는 단어를 선택한다. add 메서드가 기존값 두 개를 더하거나 이어서 새로운 값을 만든다고 가정하자. 새로 작성하는 메서드는 집합에 값 하나를 추가한다. 새 메서드는 기존 add 메서드와 맥락이 다르므로 insert나 append라는 이름이 적당하다. 새 메서드를 add라 부른다면 이는 말장난이다.   

프로그래머는 코드를 최대한 이해하기 쉽게 짜야 한다. 집중적인 탐구가 필요한 코드가 아니라 **대충 훑어봐도 이해할 코드** 작성이 목표다. 의미를 해독할 책임이 독자에게 있는 **논문 모델**이 아니라 의도를 밝힐 책임이 저자에게 있는 **잡지 모델**이 바람직하다.

**[⬆ 위로가기](#목차)**
## 해법 영역에서 가져온 이름을 사용하라
코드를 읽을 사람도 **프로그래머**라는 사실을 명심한다. 그러므로 알고리즘 이름, 패턴 이름 등을 사용해도 괜찮다. **모든 이름을 문제 영역(domain)에서 가져오는 정책**은 현명하지 못하다.   

프로그래머에게 익숙한 기술 개념은 아주 많다. **기술 개념에는 기술 이름**이 가장 적합한 선택이다.


**[⬆ 위로가기](#목차)**
## 문제 영역에서 가져온 이름을 사용하라
적절한 '프로그래머 용어'가 없다면 문제 영역에서 이름을 가져온다. 그러면 코드를 보수하는 프로그래머가 분야 전문가에게 의미를 물어 파악할 수 있다.

**[⬆ 위로가기](#목차)**
## 의미 있는 맥락을 추가하라
대다수 이름은 분명하지 않다. 그래서 클래스, 함수, 이름 공간에 넣어 맥락을 부여한다. 최후의 수단으로 접두어를 붙인다.   
'state'라는 변수는 어떤 의도로 사용됐는지 알기 어렵다. 이럴땐 아래처럼 접두어를 추가하면 분명해진다. 물론 클래스를 생성하면 더 좋다.
```typescript
let addrFirstName: string;
let addrLastName: string;
let addrState: string;
```

아래 나오는 메서드를 살펴보면 함수 이름은 맥락 일부만 제공하고 알고리즘이 나머지를 제공한다. 함수를 끝까지 읽고 나서야 number, verb, pluralModifier라는 변수 세 개가 '통계 추측'멤시지에 사용된다는 사실을 안다.
```typescript
private printGuessStatistics(candidate: string, count: number): void {
    let number: string;
    let verb: string;
    let pluralModifier: string;
    if (count === 0) {
        number = 'no';
        verb = 'are';
        pluralModifier = 's';
    } else if (count === 1) {
        number = '1';
        verb = 'is';
        pluralModifier = '';
    } else {
        number = String(count);
        verb = 'are';
        pluralModifier = 's';
    }
    let guessMessage: string = `There ${verb} ${number} ${canditate} ${pluralModifier}`;
    console.log(guessMessage);
}
```

일단 함수가 길다. GuessStatisticsMessage라는 클래스를 만들고 여기에 세 변수를 넣으면 세 변수는 **확실하게** GuessStatisticsMessage에 속한다.

```typescript
public class GuessStatisticsMessage {
    let number: string;
    let verb: string;
    let pluralModifier: string;

    public make(candidate: string, count: number): string {
        createPluralDependentMessageParts(count);
        return `There ${verb} ${number} ${canditate} ${pluralModifier}`;

    }

    private createPluralDependentMessageParts(count: number): void {
        if (count === 0) {
            thereAreNoLetters();
        } else if (count === 1) {
            thereIsOneLetter();
        } else {
            thereAreManyLetters(count);
        }
    }

    private thereAreManyLetters(count: number): void {
        number = String(count);
        verb = 'are';
        pluralModifier = 's';
    }

    private thereIsOneLetter(): void {
        number = '1';
        verb = 'is';
        pluralModifier = '';
    }

    private thereaAreNoLetters(): void {
        number = 'no';
        verb = 'are';
        pluralModifier = 's';
    }
}
```

**[⬆ 위로가기](#목차)**
## 불필요한 맥락을 없애라
고급 휘발유 충전소(Gas Station Deluxe)라는 애플리케이션을 짠다고 해서 모든 클래스 이름을 GSD로 시작하지 말자. IDE에 G를 입력하면 모든 클래스가 나오는 등 효율적이지 못하다. 

또, 접두사를 추가하는건 옳지 않다. accountAdrdress와 customerAddress보단 Address가 클래스 이름으로 적합하다.

**의미가 분명한 경우**에 일반적으로 짧은 이름이 긴 이름보다 좋다.

**[⬆ 위로가기](#목차)**
## 마치면서
다른 개발자가 반대할까봐 두려워 이름을 바꾸지 않는다면 그 생각은 고쳐라. 나름대로 이름을 바꿨다가 누군가 뭐라할지도 모른다. 그렇다고 **코드를 개선하려는 노력을 멈춰서는 안된다.**








