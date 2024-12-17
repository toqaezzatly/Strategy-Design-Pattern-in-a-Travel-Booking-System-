# Strategy Design Pattern in a Travel Booking System

## 1. Pricing Strategy

* **standard pricing** : base price 
* **discounted pricing** : how we lower the base price.
* **Dynamic pricing** : Price is governed by a many factors like availability, demand, and many more.

## 2. Implementation

**A. The Strategy Interface** Acts like a blueprint for the pricing strategy.

```python
class PricingStrategy:
    def calculate_price(self, base_price):
        '''returns the base price'''
        pass
```

**B. The Concrete Strategies**

```python
class StandardPricingStrategy(PricingStrategy):
    def calculate_price(self, base_price):
        return base_price

class DiscountedPricingStrategy(PricingStrategy):
    def __init__(self, discount_rate):
        self.discount_rate = discount_rate

    def calculate_price(self, base_price):
        return base_price * (1 - self.discount_rate)

class DynamicPricingStrategy(PricingStrategy):
    def __init__(self, availability, weather):
        self.availability = availability
        self.demand = demand
```

**  Using the Strategies in the Booking System**

```python
 class BookingSystem:
    def __init__(self, pricing_strategy):
        """Pricing strategy to be used by this system"""
        self.pricing_strategy = pricing_strategy

    def set_pricing_strategy(self, pricing_strategy):
      """Change the price strategy, can be done in real time"""
      self.pricing_strategy = pricing_strategy


    def calculate_booking_price(self, base_price):
        """Calculates price using the current pricing strategy"""
        return self.pricing_strategy.calculate_price(base_price)
```
## 3. Usage
```python
base_flight_price = 200

# Use standard pricing
standard_strategy = StandardPricing()
booking_system = BookingSystem(standard_strategy)
price = booking_system.calculate_booking_price(base_flight_price)
print(f"Price with standard pricing: ${price:.2f}")

# Use dynamic pricing
dynamic_strategy = DynamicPricing()
booking_system.set_pricing_strategy(dynamic_strategy)  #Change pricing strategy in real time
price = booking_system.calculate_booking_price(base_flight_price)
print(f"Price with dynamic pricing: ${price:.2f}")

# Use discount pricing
discount_strategy = DiscountPricing(discount_rate=0.10) # Discount of 10%
booking_system.set_pricing_strategy(discount_strategy)
price = booking_system.calculate_booking_price(base_flight_price)
print(f"Price with discount pricing: ${price:.2f}")
```


```python
Price with standard pricing: $200.00
Price with dynamic pricing: $200.00
Price with discount pricing: $180.00
```


## 3. Benefits

* **Open/Closed Principle**: You can add new pricing strategies without modifying existing code.
* **Single Responsibility Principle**: Each pricing strategy has a single responsibility and is responsible for calculating the price.
* **Dependency Inversion Principle**: You can change the pricing strategy without affecting the booking system.

* **Flexiblity**: You can add new pricing strategies without modifying existing code.

## Summary
The Strategy pattern lets us handle different pricing approaches in a clean and manageable way. We define a common interface, implement concrete strategies, and then switch between these strategies at runtime. This makes our code flexible, maintainable, and easy to extend with more pricing logic as needed. We have decoupled the process of booking from the pricing logic making our system more flexible and robust.