# DDD

## What is DDD?

Domain-Driven Design (DDD) is a software development methodology that focuses on modeling software to match a domain's complexity. It emphasizes collaboration between technical and domain experts to create a shared understanding of the domain and build software that accurately reflects its intricacies.

## Key Principles of DDD

1. **Domain**: The subject area to which the user applies a program is the domain. It is the primary focus of DDD.
2. **Ubiquitous Language**: A common language used by all team members (developers, domain experts, etc.) to ensure clear communication and understanding.
3. **Bounded Context**: A boundary within which a particular model is defined and applicable. Different models can exist in different bounded contexts.
4. **Entities**: Objects that have a distinct identity that runs through time and different states.
5. **Value Objects**: Objects that describe some characteristics or attributes but have no conceptual identity.
6. **Aggregates**: A cluster of domain objects that can be treated as a single unit.
7. **Repositories**: Mechanisms for encapsulating storage, retrieval, and search behavior which emulates a collection of objects.

## DDD Building Blocks

### Entities

Entities are objects that are defined by their identity rather than their attributes. For example, a `Customer` entity might have an ID that uniquely identifies it.

### Value Objects

Value objects are objects that are defined by their attributes. They do not have an identity. For example, a `Money` value object might have attributes like amount and currency.

### Aggregates

Aggregates are clusters of entities and value objects that are treated as a single unit. Each aggregate has a root entity, known as the aggregate root, which is responsible for ensuring the consistency of changes being made within the aggregate.

### Repositories

Repositories provide methods to access and manipulate aggregates. They act as a bridge between the domain and data mapping layers, allowing for the retrieval and storage of aggregates.

## Example of DDD Concepts

### Entity Example

```C#
public class Customer
{
    public Guid Id { get; private set; }
    public string Name { get; private set; }

    public Customer(Guid id, string name)
    {
        Id = id;
        Name = name;
    }
}
```

### Value Object Example

```C#
public class Money
{
    public decimal Amount { get; }
    public string Currency { get; }

    public Money(decimal amount, string currency)
    {
        Amount = amount;
        Currency = currency;
    }
}
```

### Aggregate Example

```C#
public class Order
{
    public Guid Id { get; private set; }
    public Customer Customer { get; private set; }
    public List<OrderItem> Items { get; private set; }

    public Order(Guid id, Customer customer)
    {
        Id = id;
        Customer = customer;
        Items = new List<OrderItem>();
    }

    public void AddItem(OrderItem item)
    {
        Items.Add(item);
    }
}
```

### Repository Example

```C#
public interface IOrderRepository
{
    Order GetById(Guid id);
    void Save(Order order);
}
```

## Conclusion

DDD is a methodology that helps manage the complexity of software development by focusing on the domain and creating a shared understanding among all stakeholders. By using entities, value objects, aggregates, and repositories, DDD ensures that the software accurately reflects the domain and is maintainable and scalable.