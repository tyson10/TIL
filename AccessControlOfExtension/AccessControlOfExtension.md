# Access contorol of extension

<aside>
💡

`extension` 앞에 명시하는 접근 제한자가 `extension` 블록 내부에 선언된 변수나 함수의 접근 레벨에 미치는 영향에 대해서 알아보자

</aside>

## 접근 레벨을 명시하지 않은 경우

```swift
public class Test {
    public init() {
        
    }
}

extension Test {
    func doSomething() {
        
    }
}
```

- 접근 레벨을 명시하지 않으면 기본적으로 `internal`임.
- 즉, `extension`도, `doSomething()`도 `internal`.

## extension에 접근 레벨 명시한 경우

```swift
public class Test {
    public init() {
        
    }
}

public extension Test {
    func doSomething() {
        
    }
}
```

- `extension`에 접근 레벨을 명시하면 내부의 `doSomething()` 함수도 해당 레벨과 동일해짐
- 아래 코드와 동일함.
    
    ```swift
    public class Test {
        public init() {
            
        }
        
        public func doSomething() {
        
        }
    }
    ```
    

## 접근 레벨을 모두 명시한 경우

```swift
public class Test {
    public init() {
        
    }
}

public extension Test {
    private func doSomething() {
        
    }
}
```

- `extension`과 내부에 선언된 변수 or 함수에 모두 접근 레벨을 명시하면 각각에서 가장 가까운 접근 레벨을 가짐.
    - `doSomething()`의 경우 `private` 접근 레벨임.