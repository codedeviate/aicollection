# Behavioral Patterns

Behavioral patterns are design patterns that deal with object collaboration and responsibility. They help in defining how objects interact and communicate with each other. Here are some common behavioral patterns with examples in a generic language:

## 1. Chain of Responsibility
Passes a request along a chain of handlers, where each handler decides either to process the request or to pass it to the next handler in the chain.

```generic
abstract class Handler {
    var successor: Handler?

    func setSuccessor(successor: Handler) {
        self.successor = successor
    }

    abstract func handleRequest(request: String)
}

class ConcreteHandler1: Handler {
    override func handleRequest(request: String) {
        if request == "Request1" {
            // Handle request
        } else if successor != nil {
            successor.handleRequest(request)
        }
    }
}

class ConcreteHandler2: Handler {
    override func handleRequest(request: String) {
        if request == "Request2" {
            // Handle request
        } else if successor != nil {
            successor.handleRequest(request)
        }
    }
}
```

## 2. Command
Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

```generic
interface Command {
    func execute()
}

class ConcreteCommand: Command {
    var receiver: Receiver

    init(receiver: Receiver) {
        self.receiver = receiver
    }

    func execute() {
        receiver.action()
    }
}

class Receiver {
    func action() {
        // Action implementation
    }
}

class Invoker {
    var command: Command

    func setCommand(command: Command) {
        self.command = command
    }

    func executeCommand() {
        command.execute()
    }
}
```

## 3. Interpreter
Defines a grammatical representation for a language and provides an interpreter to deal with this grammar.

```generic
interface Expression {
    func interpret(context: String) -> Bool
}

class TerminalExpression: Expression {
    var data: String

    init(data: String) {
        self.data = data
    }

    func interpret(context: String) -> Bool {
        return context.contains(data)
    }
}

class OrExpression: Expression {
    var expr1: Expression
    var expr2: Expression

    init(expr1: Expression, expr2: Expression) {
        self.expr1 = expr1
        self.expr2 = expr2
    }

    func interpret(context: String) -> Bool {
        return expr1.interpret(context) || expr2.interpret(context)
    }
}
```

## 4. Iterator
Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

```generic
interface Iterator {
    func hasNext() -> Bool
    func next() -> Any
}

interface Aggregate {
    func createIterator() -> Iterator
}

class ConcreteAggregate: Aggregate {
    var items: [Any] = []

    func createIterator() -> Iterator {
        return ConcreteIterator(items: items)
    }
}

class ConcreteIterator: Iterator {
    var items: [Any]
    var position: Int = 0

    init(items: [Any]) {
        self.items = items
    }

    func hasNext() -> Bool {
        return position < items.count
    }

    func next() -> Any {
        let item = items[position]
        position += 1
        return item
    }
}
```

## 5. Mediator
Defines an object that encapsulates how a set of objects interact, promoting loose coupling by keeping objects from referring to each other explicitly.

```generic
interface Mediator {
    func sendMessage(message: String, colleague: Colleague)
}

abstract class Colleague {
    var mediator: Mediator

    init(mediator: Mediator) {
        self.mediator = mediator
    }

    abstract func receiveMessage(message: String)
}

class ConcreteMediator: Mediator {
    var colleague1: Colleague1
    var colleague2: Colleague2

    func setColleague1(colleague1: Colleague1) {
        self.colleague1 = colleague1
    }

    func setColleague2(colleague2: Colleague2) {
        self.colleague2 = colleague2
    }

    func sendMessage(message: String, colleague: Colleague) {
        if colleague === colleague1 {
            colleague2.receiveMessage(message)
        } else {
            colleague1.receiveMessage(message)
        }
    }
}

class Colleague1: Colleague {
    override func receiveMessage(message: String) {
        // Handle message
    }
}

class Colleague2: Colleague {
    override func receiveMessage(message: String) {
        // Handle message
    }
}
```

## 6. Memento
Captures and externalizes an object’s internal state without violating encapsulation, so that the object can be restored to this state later.

```generic
class Memento {
    var state: String

    init(state: String) {
        self.state = state
    }

    func getState() -> String {
        return state
    }
}

class Originator {
    var state: String

    func setState(state: String) {
        self.state = state
    }

    func getState() -> String {
        return state
    }

    func saveStateToMemento() -> Memento {
        return Memento(state: state)
    }

    func getStateFromMemento(memento: Memento) {
        state = memento.getState()
    }
}

class Caretaker {
    var mementoList: [Memento] = []

    func add(state: Memento) {
        mementoList.append(state)
    }

    func get(index: Int) -> Memento {
        return mementoList[index]
    }
}
```

## 7. Observer
Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

```generic
interface Observer {
    func update()
}

class ConcreteObserver: Observer {
    var observerState: String

    func update() {
        // Update state
    }
}

class Subject {
    var observers: [Observer] = []

    func attach(observer: Observer) {
        observers.append(observer)
    }

    func detach(observer: Observer) {
        observers.removeAll { $0 === observer }
    }

    func notifyObservers() {
        for observer in observers {
            observer.update()
        }
    }
}
```

## 8. State
Allows an object to alter its behavior when its internal state changes, appearing to change its class.

```generic
interface State {
    func handle(context: Context)
}

class ConcreteStateA: State {
    func handle(context: Context) {
        context.setState(state: ConcreteStateB())
    }
}

class ConcreteStateB: State {
    func handle(context: Context) {
        context.setState(state: ConcreteStateA())
    }
}

class Context {
    var state: State

    init(state: State) {
        self.state = state
    }

    func setState(state: State) {
        self.state = state
    }

    func request() {
        state.handle(context: self)
    }
}
```

## 9. Strategy
Defines a family of algorithms, encapsulates each one, and makes them interchangeable, allowing the algorithm to vary independently from clients that use it.

```generic
interface Strategy {
    func execute()
}

class ConcreteStrategyA: Strategy {
    func execute() {
        // Implementation of algorithm A
    }
}

class ConcreteStrategyB: Strategy {
    func execute() {
        // Implementation of algorithm B
    }
}

class Context {
    var strategy: Strategy

    func setStrategy(strategy: Strategy) {
        self.strategy = strategy
    }

    func executeStrategy() {
        strategy.execute()
    }
}
```

## 10. Template Method
Defines the skeleton of an algorithm in a method, deferring some steps to subclasses without changing the algorithm’s structure.

```generic
abstract class AbstractClass {
    func templateMethod() {
        primitiveOperation1()
        primitiveOperation2()
    }

    abstract func primitiveOperation1()
    abstract func primitiveOperation2()
}

class ConcreteClass: AbstractClass {
    override func primitiveOperation1() {
        // Implementation of primitive operation 1
    }

    override func primitiveOperation2() {
        // Implementation of primitive operation 2
    }
}
```

## 11. Visitor
Represents an operation to be performed on the elements of an object structure, allowing new operations to be defined without changing the classes of the elements on which it operates.

```generic
interface Visitor {
    func visit(element: Element)
}

interface Element {
    func accept(visitor: Visitor)
}

class ConcreteElementA: Element {
    func accept(visitor: Visitor) {
        visitor.visit(element: self)
    }
}

class ConcreteElementB: Element {
    func accept(visitor: Visitor) {
        visitor.visit(element: self)
    }
}

class ConcreteVisitor: Visitor {
    func visit(element: Element) {
        // Implementation of visit operation
    }
}
```

These patterns help in defining clear and maintainable interactions between objects, promoting flexibility and reusability in the design.