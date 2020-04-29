## AIRLINE RESERVATION SOFTWARE

#### Problem Statement

<div style="text-align: justify">There are three types of flights based on different types of seats available. Type 1: Economy Tickets; Type 2: Business Tickets and Type 3: First Class Tickets. A flight provides a row of seats in each of the Types mentioned above with a passage dividing each row in the middle. Each row may consist of two(A,B) or four(A,B,C.D) or six (A,B,C,D,E,F) seats. In a Type 1 flight, all rows for economy class and will consist of a maximum of 6 seats per row. In a Type 2 flight, rows numbered 1 to 10 are for business class and will consist of a maximum of 4 seats per row. In a type 3 flight, rows numbered 1 to 10 are for first class and will consist of a maximum of two seats per row and rows 11 to 20 are for business class with a maximum of 4 seats per row. In a type 2 flight, Economy rows are from row 11 onwards and in a type 3 flight, row number 21 onwards is for Economy class.  An Economy fare passenger can check in a maximum of 15Kgs; a Business class passenger, 25 Kgs and a First Class passenger, 30 Kgs.  Excess baggage may be purchased by a passenger based on the following norms: 15 plus to 20 Kgs for Economy by paying Rs.2000 per additional Kg; 25 plus to 35 Kgs for Business class by paying Rs.3000 per additional Kg and 30 plus Kgs to 40 Kgs for First class by paying Rs.4000 per additional Kg. </div>

---

#### Solution

##### Introduction to the designed ARS

<div style = "text-align: justify">An ARS(Airline Reservation Software) is a simple application used by people for travelling purposes. Its basic operation is to book a ticket in the required transportation. But the recent applications also performs other operations such as cancelling the ticket, showing the details of already booked tickets, showing the list of passengers who have booked the tickets, showing the minimum weight allowed and the extra payment to be done if he/she wants to carry  more weight, etc. The application designed here is a simple model of the same software. </div>

![1](https://imgur.com/gK76g4Q.png)

![2](https://imgur.com/Tj1shCr.png)

​		According to the designed application, first the screen displays the operations that are available. They are Booking, Cancelling, Displaying ticket of a particular passenger, displaying the name, PNR number, flight type and seat number of the all passengers who have booked ticket and exit. 

​		For **Booking** a ticket the authority needs to input the name, type of flight the customer wants to travel in, the type of seat he/she wants to reserve. Then the person’s seat gets allotted and a PNR gets generated. After this, the person needs to input the weight of his baggage. Then he can see the minimum amount of baggage he is allowed. If the weight of the baggage is more than the minimum limit but less than maximum limit, then he needs to make an extra payment. If the weight is exceeding the maximum limit, then he needs to reduce the weight he needs to carry.

​		For **Cancelling** the ticket the authority only need to enter the PNR of the passenger that was generated during the booking, and the booking gets cancelled.

​		For **Displaying** the ticket of a particular passenger, we need to enter the PNR of the passenger that was generated during the booking, and then we can see the details of the seat that was booked. 

​		If u want to see the **Details of all Passengers** who have booked, then we can see the name, PNR number, type of flight booked and the seat allotted for all the passengers.



##### Below is the application designed for the above ARS

```java
import java.io.*;
import java.util.*;
import java.lang.*;
class Type1 extends Airlines{
	static String name;
	static int k;
	Type1(String name) {
		this.name = name;
	}
	public static void book(){	
		Scanner inp = new Scanner(System.in);
		NAME.add(name);
		TYPE.add(1);
		SEAT.add('E');
		Random rand = new Random();
		int no = rand.nextInt(180)+1;
		int pnr = rand.nextInt(90000);
		PNR.add(pnr);
		NUM.add(no);
		System.out.println("\nPassenger Details");
		System.out.println("Name : "+name);
		System.out.printf("PNR : %05d\n",pnr);
		System.out.println("Flight : Type 1 (Economy)");
		System.out.println("Seat No. : "+no);
		System.out.print("Enter the Baggage Weight(Kg) : ");
		int w = inp.nextInt();
		String p = Integer.toString(pnr);
		System.out.println("The Baggage weight allowed is : "+getBaggageLimit(p));
		k = w-getBaggageLimit(p);
		makePayment(k);
	}
	public static int buyExcessBaggage(int k) {
		if (k<=0)
			return 0;
		else if (k>0 && k<=5)
			return k;
		else
			return -1;
	}
	public static void makePayment(int R) {
		if (buyExcessBaggage(R)==0)
			System.out.println("Baggage weight is within Limits!!!");
		else if (buyExcessBaggage(R)==-1)
			System.out.println("Baggage weight is out of Limits, Reduce the Weight!!!");
		else
			System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*2000);
	}
}

class Type2 extends Airlines{
	static String name;
	static char seat;
	static int k;
	Type2(String name) {
		this.name = name;
	}
	public static void book(){
		Scanner inp = new Scanner(System.in);
		System.out.print("Enter Seat(E,B) : ");
		seat = inp.next().charAt(0);
		TYPE.add(2);
		NAME.add(name);
		Random rand = new Random();
		int pnr = rand.nextInt(90000);
		PNR.add(pnr);
		System.out.println("\nPassenger Details");
		System.out.println("Name : "+name);
		System.out.printf("PNR : %05d\n",pnr);
		int no;
		if (seat == 'E') {
			System.out.println("Flight : Type 2 (Economy)");
			SEAT.add('E');
			no = rand.nextInt(120)+1;
			NUM.add(no);
		}
		else {
			System.out.println("Flight : Type 2 (Buissness)");
			SEAT.add('B');
			no = rand.nextInt(40)+121;
			NUM.add(no);
		}			
		System.out.println("Seat No. : "+no);
		System.out.print("Enter the Baggage Weight(Kg) : ");
		int w = inp.nextInt();
		String p = Integer.toString(pnr);
		System.out.println("The Baggage weight allowed is : "+getBaggageLimit(p));
		k = w-getBaggageLimit(p);
		makePayment(k);
	}
	public static int buyExcessBaggage(int k) {
		if (seat == 'E') {
			if (k<=0)
				return 0;
			else if (k>0 && k<=5)
				return k;
			else
				return -1;
		}
		else {
			if (k<=0)
				return 0;
			else if (k>0 && k<=10)
				return k;
			else
				return -1;
		}
	}
	public static void makePayment(int R) {
		if (buyExcessBaggage(R)==0)
			System.out.println("Baggage weight is within Limits!!!");
		else if (buyExcessBaggage(R)==-1)
			System.out.println("Baggage weight is out of Limits, Reduce the Weight!!!");
		else {
			if(seat == 'E')
				System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*2000);
			else
				System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*3000);
		}
	}
}

class Type3 extends Airlines{
	static String name;
	static char seat;
	static int k;
	Type3(String name) {
		this.name = name;
	}
	public static void book(){
		Scanner inp = new Scanner(System.in);
		System.out.print("Enter Seat(E,B,F) : ");
		seat = inp.next().charAt(0);
		TYPE.add(3);
		NAME.add(name);
		Random rand = new Random();
		int pnr = rand.nextInt(10000);
		PNR.add(pnr);
		System.out.println("\nPassenger Details");
		System.out.println("Name : "+name);
		System.out.printf("PNR : %05d\n",pnr);
		int no;
		if (seat == 'E') {
			System.out.println("Flight : Type 3 (Economy)");
			SEAT.add('E');
			no = rand.nextInt(60)+1;
			NUM.add(no);
		}
		else if (seat == 'B') {
			System.out.println("Flight : Type 3 (Buissness)");
			SEAT.add('B');
			no = rand.nextInt(40)+61;
			NUM.add(no);
		}
			
		else {
			System.out.println("Flight : Type 3 (First Class)");
			SEAT.add('F');
			no = rand.nextInt(20)+101;
			NUM.add(no);
		}
		System.out.println("Seat No. : "+no);
		System.out.print("Enter the Baggage Weight(Kg) : ");
		int w = inp.nextInt();
		String p = Integer.toString(pnr);
		System.out.println("The Baggage weight allowed is : "+getBaggageLimit(p));
		k = w-getBaggageLimit(p);
		makePayment(k);
	}
	public static int buyExcessBaggage(int k) {
		if (seat == 'E') {
			if (k<=0)
				return 0;
			else if (k>0 && k<=5)
				return k;
			else
				return -1;
		}
		else{
			if (k<=0)
				return 0;
			else if (k>0 && k<=10)
				return k;
			else
				return -1;
		}
	}
	public static void makePayment(int R) {
		if (buyExcessBaggage(R)==0)
			System.out.println("Baggage weight is within Limits!!!");
		else if (buyExcessBaggage(R)==-1)
			System.out.println("Baggage weight is out of Limits, Reduce the Weight!!!");
		else {
			if(seat == 'E')
				System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*2000);
			else if (seat == 'B')
				System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*3000);
			else
				System.out.println("Baggage is more than minimum weight Please pay : "+buyExcessBaggage(R)*4000);
		}
	}
}

public class Airlines {
	static ArrayList<String> NAME = new ArrayList<String>();
	static ArrayList<Integer> PNR = new ArrayList<Integer>();
	static ArrayList<Integer> NUM = new ArrayList<Integer>();
	static ArrayList<Integer> TYPE = new ArrayList<Integer>();
	static ArrayList<Character> SEAT = new ArrayList<Character>();
	static int count = 0;
	public static void display() {
		System.out.println("\nNAME\tPNR\tFLIGHT\tSEAT");
		for (int i = 0; i <count; i++){
System.out.printf("%s\t%05d\t%d\t%c%d\n",NAME.get(i),PNR.get(i),TYPE.get(i),SEAT.get(i),NUM.get(i));
        } 
	public static void Remove(int rem) {
		try {
		int i = PNR.indexOf(rem);
		PNR.remove(i);
		TYPE.remove(i);
		SEAT.remove(i);
		NAME.remove(i);
		NUM.remove(i);
		count = count - 1;
		}
		catch(Exception e) {
			System.out.println("Sorry booking not found!!!");
		}
	}
	public static int getBaggageLimit(String pnr) {
		int p = Integer.parseInt(pnr);
		int i = PNR.indexOf(p);
		char S = SEAT.get(i);
		if (S == 'E')
			return 15;
		else if(S == 'B')
			return 25;
		else 
			return 30;
	}
	public static void ticket(int pnr) {
		try {
		int i = PNR.indexOf(pnr);
		System.out.println("\nPassenger Details");
		System.out.println("Name : "+NAME.get(i));
		System.out.printf("PNR : %05d\n",pnr);
		System.out.println("Flight : "+ TYPE.get(i));
		System.out.println("Seat Number : "+SEAT.get(i)+NUM.get(i));
		}
		catch(Exception e) {
			System.out.println("Sorry booking not found!!!");
		}
	}
	public static void main(String[] args) {
		System.out.println("\n\t\t\t***AIRLINES RESERVATION SYSTEM***\n");
		Scanner inp = new Scanner(System.in);
		System.out.println("1. Booking\t2. Cancel\t3. Display Ticket\t4. Display Passengers\t5. Exit");
		System.out.print("\nEnter choice : ");
		int choice = inp.nextInt();
		
		while(choice !=5) {
			if (choice == 1) {
				count = count + 1;
				System.out.print("Enter Name : ");
				String name = inp.next();
				System.out.println("\nAIRLINES\nFlight 1 : Economy\nFlight 2 : Economy Buissness\nFlight 3 : Economy Buissness First_Class");
				System.out.print("Enter Flight Type : ");
				int type = inp.nextInt();
				
				Type1 o = new Type1(name);
				Type2 t = new Type2(name);
				Type3 h = new Type3(name);
				
				if (type == 1)
					o.book();
				else if (type == 2)
					t.book();
				else if (type == 3)
					h.book();
				else
					System.out.print("Flight Currently not availale!!!");
			}
			
			else if (choice == 2) {
				System.out.print("Enter PNR number : ");
				int rem = inp.nextInt();
				Remove(rem);
			}
			else if (choice == 3) {
				System.out.print("Enter PNR number : ");
				int pnr = inp.nextInt();
				ticket(pnr);
			}
			else if (choice == 4)
				display();
			else
				System.out.print("Enter correct choice");
			
			System.out.println("\n1. Booking\t2. Cancel\t3. Display Ticket\t4. Display Passengers\t5. Exit");
			System.out.print("\nEnter choice : ");
			choice = inp.nextInt();
		}
		System.out.print("\nThank You!!!");
	}
}


```



##### Following is the output obtained for the above code

> Output:

![](https://imgur.com/vfUhGeV.png)

![](https://imgur.com/0TAJV8h.png)

![](https://imgur.com/LumjyAn.png)

![](https://imgur.com/b9u4El0.png)





