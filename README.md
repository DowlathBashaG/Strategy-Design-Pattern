# Strategy-Design-Pattern



Strategy Design Pattern :

		-The Strategy Pattern is a behavioral design pattern.
		-It allows you to define a family of algorithms, encapsulate each one, and make them interchangeable.
		-Strategy Pattern lets you choose algorithms (strategies) at runtime.
		-It helps in clean coding, reduces conditional logic, and makes the system flexible.

New behaviors can be added without modifying existing classes.

Main Goal:

		Let the algorithm vary independently from the clients that use it.

		Remove if-else or switch-case based decision making.

		Change behavior of an object at runtime.

Real-world Example:

		Suppose you are developing a Navigation App (like Google Maps).
		
		Users can choose between:

		Car Route

		Walking Route

		Public Transport Route

Each route calculation is different.

		Using Strategy Pattern, we can easily switch between strategies without changing the app's code.
		
		
Components of Strategy Pattern:

		Part															Description
		
		Strategy Interface									Common interface for all strategies
		Concrete Strategies									Different implementations of the strategy
		Context Class										Uses a strategy object to perform the action
		

Let's build a simple payment system example in Java using the Strategy Pattern.

Payment System:
--------------

Step 1: Create the Strategy Interface

			// PaymentStrategy.java
			public interface PaymentStrategy {
				void pay(int amount);
			}

Step 2: Create Concrete Strategies

			// CreditCardPayment.java
			public class CreditCardPayment implements PaymentStrategy {
				private String cardNumber;

				public CreditCardPayment(String cardNumber) {
					this.cardNumber = cardNumber;
				}

				@Override
				public void pay(int amount) {
					System.out.println(amount + " paid with credit card: " + cardNumber);
				}
			}

			// PayPalPayment.java
			public class PayPalPayment implements PaymentStrategy {
				private String emailId;

				public PayPalPayment(String emailId) {
					this.emailId = emailId;
				}

				@Override
				public void pay(int amount) {
					System.out.println(amount + " paid using PayPal account: " + emailId);
				}
			}


Step 3: Create the Context Class


			// ShoppingCart.java
			public class ShoppingCart {
				private PaymentStrategy paymentStrategy;

				// Set the payment strategy
				public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
					this.paymentStrategy = paymentStrategy;
				}

				// Perform payment
				public void checkout(int amount) {
					if (paymentStrategy == null) {
						throw new IllegalStateException("PaymentStrategy not set");
					}
					paymentStrategy.pay(amount);
				}
			}


Step 4: Test the Strategy Pattern

		// Main.java
		public class Main {
			public static void main(String[] args) {
				ShoppingCart cart = new ShoppingCart();

				// Pay with Credit Card
				cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9012-3456"));
				cart.checkout(1000);

				// Switch to PayPal
				cart.setPaymentStrategy(new PayPalPayment("user@example.com"));
				cart.checkout(500);
			}
		}


Output :

		1000 paid with credit card: 1234-5678-9012-3456
		500 paid using PayPal account: user@example.com
		

Why Use Strategy Pattern?


			Advantage									Reason
			
			Open/Closed Principle						Add new strategies without changing existing code
			Eliminate If-Else/Switch					No messy conditional code
			Easy to Switch Behavior						Set different strategy at runtime easily
			Cleaner Code								Each strategy class handles only one type of behavior
			
			
Real-World Examples of Strategy Pattern

			Where	Example
			
			Games	Different player movement algorithms (aggressive, defensive)
			Payment Systems	PayPal, Credit Card, Bank Transfer, Cryptocurrency
			Compression Algorithms	Zip, Rar, Tar
			Sorting Algorithms	Bubble Sort, Merge Sort, Quick Sort selected dynamically
			
			
