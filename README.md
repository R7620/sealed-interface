# sealed-interface
Develop a scenario based program by using interface for processing the payment  using different available options like Credit Card and Debit Card and UPI Payment. Provide loose coupling through interface.

package com.raj.inte.blc;
public  sealed  interface Payment  permits CreditCardPayment ,DebitCardPayment,UPIPayment
{
void MakePayment(double amount);
void makeRefund(double amount);
}
package com.raj.inte.blc;

public final class CreditCardPayment   implements Payment
{
private String cardHolderName;



public CreditCardPayment(String cardHolderName) {
	super();
	this.cardHolderName = cardHolderName;
}

@Override
public void MakePayment(double amount) 
{
	System.out.println("Starting checkout for amount RS :"+amount);
	System.out.println("Paid Rs :"+amount +" using Credit Card Holder :"+cardHolderName );
	
}

@Override
public void makeRefund(double amount) 
{
	System.out.println("Order Canceled. Initiating Refund...");
	System.out.println("Cancelling order for amount RS :"+amount);
	System.out.println("Refunded Rs :"+amount +" to Credit Card Holder :"+cardHolderName);
}

}
package com.raj.inte.blc;

public final class DebitCardPayment implements Payment
{
private String bankName;


	public DebitCardPayment(String bankName) {
	super();
	this.bankName = bankName;
}

	@Override
	public void MakePayment(double amount) 
	{
		System.out.println("Starting checkout for amount RS :"+amount);
		System.out.println("Paid RS "+amount+"using Debit Card Bank:"+bankName);
	}

	@Override
	public void makeRefund(double amount) {
		System.out.println(" Order Canceled. Initiating Refund...");
		System.out.println("Cancelling order for amount RS :"+amount);
		System.out.println("Refunded RS :"+amount+ "to Debit Card Bank:"+bankName);
	}

}
package com.raj.inte.blc;

public  final class UPIPayment  implements Payment
{
	private String upiid;
	

	public UPIPayment(String upiid) {
		super();
		this.upiid = upiid;
	}

	@Override
	public void MakePayment(double amount) 
	{
		
	System.out.println("Starting checkout for amount RS :"+amount);
	System.out.println("Paid RS"+amount +"using UPI ID :"+upiid);
	
	}

	@Override
	public void makeRefund(double amount) 
	{
		
		System.out.println("Order Canceled. Initiating Refund...");
		System.out.println("Cancelling order for amount RS "+amount);
		System.out.println("Refunded RS : "+amount+"to UPI ID :"+upiid);
	}

}
package com.raj.inte.blc;

public class ShoppingCart {
 private double totalAmount;

public ShoppingCart(double totalAmount) {
	super();
	this.totalAmount = totalAmount;
}
 
 public void checkOut(Payment payment) 
 {
	  payment.MakePayment(totalAmount);
 }
 public void CancleOrder(Payment payment) {
	 payment.makeRefund(totalAmount);
 }
 
}
package com.raj.elc;

import java.util.Scanner;

import com.raj.inte.blc.CreditCardPayment;
import com.raj.inte.blc.DebitCardPayment;
import com.raj.inte.blc.Payment;
import com.raj.inte.blc.ShoppingCart;
import com.raj.inte.blc.UPIPayment;

public class Customer {

	public static void main(String[] args) 
	{
		Scanner sc=new Scanner(System .in);
		
		System.out.println("Enter your total bill Amount");
		int Amount=sc.nextInt();
		Payment payment=null;
		ShoppingCart shop=null;
		
		
		System.out.println("choose payment Method ");
		
		int choise=sc.nextInt();
		System.out.println("1. Credit Card");
		System.out.println(" 2. Debit Card");
		System.out.println("3. UPI");
		switch(choise) {
		case  1 :
			payment=new CreditCardPayment(" MR. Ravi");
			shop=new ShoppingCart(Amount);
			shop.checkOut(payment);
		   shop.CancleOrder(payment);
		   break;
		case  2 :
			payment=new DebitCardPayment("State Bank of India");
			shop=new ShoppingCart(Amount);
			shop.checkOut(payment);
		   shop.CancleOrder(payment);
		   break;
		case 3 :
			payment=new UPIPayment("reach_scott@upi");
			shop=new ShoppingCart(Amount);
			shop.checkOut(payment);
		   shop.CancleOrder(payment);
		   
		
			sc.close();
		}
		
		
		

	}

}




