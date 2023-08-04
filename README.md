<br/>

## `Codable` protocol 

<br/>



### 01. Codable 이란 무엇인가요?

- Codable은 Encodable 과 Decodable이 합쳐진 것을 의미합니다
- **Encodable**이란 데이터를 Encoder 에서 변환해주려는 프로토콜로 바꿔주는 것입니다
- **Decodable**이란 데이터를 원하는 모델로 Decode 해주는 것입니다
- 예시) **Encodable -> 모델을 json으로 인코드 / Decodable -> json을 내가 원하는 모델로 디코드**

<br/><br/>

### 02. UserDefualts 의 데이터를 저장하는 방법으로 Codable 프로토콜을 사용한 이유는 무엇인가요?

- `Codable` 프로토콜을 사용한 이유의 가장 큰 이유는 간결함입니다
- UserDefault는 key-value 데이터이기 때문에 todo 데이터의 양이 늘어나면 Key값을 단순 나열하는 형태가 되어버립니다. 즉 UserDefaults는 Class나 Struct를 직접 다루지 못한다는 한계를 가지고 있습니다
- `Codable` 을 통해서 Todo 아이템 배열 데이터를 구조체로  encdoe 할 수 있었습니다.
- 이러한 구조체 데이터를 통해 간결성, 유연성, 가독성이라는 세마리 토끼를 잡을 수 있었습니다
- 아래 코드를 통해 비교해보겠습니다

```Swift
// Codable 프로토콜을 채택했을 경우

//struct를 통한 데이터 관리
struct ToDoItem: Codable {
    let title: String
}

var toDoItems = TodDoItem()

// Encoding 
if let encodedData = try? JSONEncoder().encode(toDoItems) {
    UserDefaults.standard.set(encodedData, forKey: "toDoItems")
}

// Decoding 
if let savedData = UserDefaults.standard.data(forKey: "toDoItems"),
   let decodedItems = try? JSONDecoder().decode([ToDoItem].self, from: savedData) {
    toDoItems = decodedItems
}
```
```swift
// Codable 프로토콜을 채택했을 경우

//struct를 통한 데이터 관리
struct ToDoItem: Codable {
    let title: String
}

var toDoItems = TodDoItem()

// Encoding 
if let encodedData = try? JSONEncoder().encode(toDoItems) {
    UserDefaults.standard.set(encodedData, forKey: "toDoItems")
}

// Decoding 
if let savedData = UserDefaults.standard.data(forKey: "toDoItems"),
   let decodedItems = try? JSONDecoder().decode([ToDoItem].self, from: savedData) {
    toDoItems = decodedItems
}
```
