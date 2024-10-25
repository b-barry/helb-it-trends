---
title: If-Else Replacement : Factory and Strategy
pubDate: Oct 25, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Java
  - Design Patterns
  - Methodology
imgUrl: '../../assets/java-design-patterns.jpg' 
description: If-else blocks get quite confusing as a project gets larger and larger. However, there's a simple solution which we could use to get rid of those blocks. Just use Strategy and Facotry patterns together !
layout: '../../layouts/BlogPost.astro'
---
# If-Else Replacement : Factory and Strategy
---
Oftentimes, when building our applications, we face the challenge of supporting different types of behaviours for a same workflow, for example, a payment functionality supporting different methods.

Maintaining such a code means that it must be scaled to support new methods as they grow, enlarging the size of the if-else blocks. The resulting code is hard to manage, and looks like this:

```java
public class PaymentService {

    public void processPayment(String paymentType) {
        if (paymentType.equals("CREDIT_CARD")) {
            System.out.println("Processing credit card payment...");
        } else if (paymentType.equals("DEBIT_CARD")) {
            System.out.println("Processing debit card payment...");
        } else if (paymentType.equals("CRYPTO")) {
            System.out.println("Processing crypto payment...");
        } else {
            throw new IllegalArgumentException("Invalid payment type");
        }
    }
}

```

Using a combination of Strategy and Factory could solve this scalability problem.

Firstly, let's regroup the different types under an enum type:

```java
public enum PaymentType {
    CREDIT_CARD,
    DEBIT_CARD,
    CRYPTO
}
```

Then, let's define a Strategy interface and its implementing classes:

```java
public interface PaymentStrategy {
    void pay(PaymentRequest request);
}

public class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay(PaymentRequest request) {
        System.out.println("Processing $type payment".replace("$type", String.valueOf(request.getPaymentType())));
    }
}

public class DebitCardPayment implements PaymentStrategy {
    @Override
    public void pay(PaymentRequest request) {
        System.out.println("Processing $type payment".replace("$type", String.valueOf(request.getPaymentType())));
    }
}

public class CryptoPayment implements PaymentStrategy {
    @Override
    public void pay(PaymentRequest request) {
        System.out.println("Processing $type payment".replace("$type", String.valueOf(request.getPaymentType())));
    }
}

```

Now, using the Factory pattern will help us determine the strategy to adopt:

```java
public class PaymentFactory {
    private static final Map<PaymentType, PaymentStrategy> strategies = new EnumMap<>(PaymentType.class);

    static {
        strategies.put(PaymentType.CREDIT_CARD, new CreditCardPayment());
        strategies.put(PaymentType.DEBIT_CARD, new DebitCardPayment());
        strategies.put(PaymentType.CRYPTO, new CryptoPayment());
    }

    public static PaymentStrategy getPaymentStrategy(PaymentType paymentType) {
        PaymentStrategy strategy = strategies.get(paymentType);

        if (Objects.isNull(strategy))
            throw new IllegalArgumentException("Strategy not found");

        return strategy;
    }
}
```
Finally, we can use the built structure by requesting for a specific type of payment method, and let the app deal with the rest :

```java
public class PaymentService {

    public void processPayment(PaymentRequest request) {
        // Don't forget to check objects if null!
        if (Objects.isNull(request) || Objects.isNull(request.getPaymentType())
            throw new IllegalArgumentException("Request can not be null!");
        PaymentStrategy strategy = PaymentFactory.getPaymentStrategy(request.getPaymentType());

        strategy.pay(request);
    }
}
```
Not only did we get rid of if-else statements and blocks, but the code itself became more modular and extensible.

The main advantages of this process are :
- **Extensibility**: Adding a new strategy only takes a few lines of code
- **Readability**: The resulting separated code is more easily managed and understood
- **Maintainability**: It's possible to change the code in one part (strategy or factory) without spreading effects to other parts of the code

## Sources

- <https://www.digitalocean.com/community/tutorials/java-design-patterns-example-tutorial> (Cover Image)
- <https://dev.to/tamerardal/dont-use-if-else-blocks-anymore-use-strategy-and-factory-pattern-together-4i77>
