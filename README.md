THIS IS MY UPDATED ANSWER SINCE ABOVE ANSWER IS UN EDITABLE. 

OO Three main features

ENCAPSULATION:

In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class. Therefore, it is also known as data hiding.

In other words, encapsulation is hiding of data for it to not access directly and uncontrollably, in order to control it, you have to make sure your elements(or variables) are private and has a setter and getter in order for you to control the data manipulation of it.

Example of setting up your encapsulated class.

````
public class EncapsulatedClass {
   private String name;
   private int age;


   public constructClass(){
	}
   public int getAge() {
      return age;
   }

   public String getName() {
      return name;
   }

   public void setAge( int newAge) {
      age = newAge;
   }

   public void setName(String newName) {
      name = newName;
   }
}
````

Example of accessing your encapsulated class:

````
public void set_and_get_data_from_encapsulated_class{
	EncapsulatedClass encapsulatedClass = new constructClass();
	encapsulatedClass.setAge(19);
	encapsulatedClass.setName("Robert Najib");
	
	System.out.println("Hi! My name is " +getName+" and I am "+getName+" years old");
}
````
INHERITANCE:

 Inheritance is a mechanism in which one object acquires all the properties and behaviors of a parent object. It is an important part of OOPs (Object Oriented programming system).
 
 In inheritance, there are some commonly used terms like in below:
	Class: A class is a group of objects which have common properties. It is a template or blueprint from which objects are created.
	Sub Class/Child Class: Subclass is a class which inherits the other class. It is also called a derived class, extended class, or child class.
	Super Class/Parent Class: Superclass is the class from where a subclass inherits the features. It is also called a base class or a parent class.
	Reusability: As the name specifies, reusability is a mechanism which facilitates you to reuse the fields and methods of the existing class when you create a new class. You can use the same fields and methods already defined in the previous class.
	
Example: 
````
class Employee{  
 float salary=50000;  
}  

class Programmer extends Employee{  
 int bonus=10000;  
 public static void main(String args[]){  
   Programmer p=new Programmer();  
   System.out.println("Programmer salary is:"+p.salary);  
   System.out.println("Bonus of Programmer is:"+p.bonus);  
}  
}  
````

As you can see, Programmer can access the declaration of class Employee which is summary with just extending the class Employee into Programmer class.
And that's one example of inheritance. 
In here the Class are Employee and Programmer, Sub/Child Class is the Programmer and Super/Parent Class is Employee.
You are free to use the class Employee to other child class if you want to by just extending it.

POLYMORPHISM:

Polymorphism means "many forms", and it occurs when we have many classes that are related to each other by inheritance.
If Inheritance lets us inherit attributes and methods from another class. Polymorphism uses those methods to perform different tasks. This allows us to perform a single action in different ways.

We can take the sounds of an animal as an example for us to easily understand polymorphism.

Example:

````
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}

class MyMainClass {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();
    Animal myPig = new Pig();
    Animal myDog = new Dog();
        
    myAnimal.animalSound();
    myPig.animalSound();
    myDog.animalSound();
  }
}

//OUTPUT
The animal makes a sound
The pig says: wee wee
The dog says: bow wow
````

In above example, we reused the method animalSound() from Animal class to produce a different animal sounds with the same method name which is animalSound().
 

 Five principles(SOLID)
 
 
S ingle Responsibility:
Per reading the documentation of SOLID principles, Single Responsibility is the most easier to understand because the definition of it is pretty basic.
A class should do one and only one job.
	
Below is the example of bad practice of Single Responsibility
	
`````
	public class TechnicalStaff {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
    void maintainSystems(){}
    void performAppraisal(){}
    void promoteEmployee(){}
	}
````
	
As you can see to above code, TechnicalStaff class has a lot of job to do. There are the personal information of the staff, Employee's description, performance Appraisal etc. Employee cannot promote it self, so it is better to move it to other class. Also, this would make your heir confused to your codes, and might take a hard time to reuse the class.
	
Below is the refactored version of the above codes that follows Single Responsibility Principle.
	
````
	public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
	}
	public class TechnicalStaff extends Employee {
    void maintainSystems(){} 
	}
	public class Manager extends Employee {
    void performAppraisalOfDirectReport(TechnicalStaff employee){}
    void promoteDirectReport(TechnicalStaff employee){}
	}
````
	

O pen for Extension/Closed for Modification

Like the acronym Meaning of this, the meaning of it is Software entities (classes, modules, functions, etc.)  should be Open for extension, but closed for modification.
	 
Below is a good example of Open for Extension/Closed for Modification,
Let us reuse the good example of Single Responsibility above then I'll explain to you our current principle in it.
	 
````
	public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
	}
	public class TechnicalStaff extends Employee {
    void maintainSystems(){} 
	}
	
	//Added Class
	public class Accountant extends Employee {
    void maintainAccounts(){}
	}
	//end of Added Class
	
	public class Manager extends Employee {
    void performAppraisalOfDirectReport(Employee employee){}
    void promoteDirectReport(Employee employee){}
	}
````
	
As you can see, in this kind of structure, we can easily add another job description that is under a Manager which is accountant. 
We don't have to modify the Manager class as it can handle both the technicalStaff and Accountant as long as they extends the Employee class. 
Manager can now do PerformAppraisalOfDirectReport/promoteDirectReport for both Accountant and Technical Staff.			

L iskov Substitution

A child class must be able to completely substitute and act-in for it’s base(parent) class.
	
Say, anyone from Manager and above in the hierarchy is allowed to send communication messages in their own way to their direct and indirect reports down the hierarchy.
	
````
	public abstract class Employee {
    private int id;
    private String fname, lname, title;
    private Date dob, dateOfJoining;
    //Getters & setters
    ...
	}
	public abstract class ManagementStaff extends Employee {
		void performAppraisalOfDirectReport(Employee employee){}
		void promoteDirectReport(Employee employee){}    
		abstract void sendCommunication();
	}
	public class TechnicalStaff extends Employee {
		void maintainSystems(){}
	}
	public class Accountant extends Employee {
		void maintainAccounts(){}
	}
	public class Manager extends ManagementStaff {
		void sendCommunication(){} //action allowed
	}
	public class Director extends ManagementStaff {
		void sendCommunication(){} //action allowed
	}
````
	
As you can see to the above code, we created an abstract class ManagementStaff that do the performAppraisalOfDirectReport and promoteDirectReport that can be used by either Director or Manager or whoever you want that qualifies to do that action. 

I nterface Segregation
	
Clients should not be forced to depend upon interfaces that they do not use
	
Similar to the Single Responsibility Principle, the goal of the Interface Segregation Principle is to reduce the side effects and frequency of required changes by splitting the software into multiple, independent parts.
	
````
	public interface Reader {
    Read(b []byte) (n int, err error) 
	}
	public interface Writer  {
		Write(b []byte)(n int, err error) 
	}
	public interface Trimmer  {
		Trim(b []byte, exclusions string)[]byte 
	}
````
	
As you can see, we splitted Reader, Writer and Trimmer interface into three instead of combining it into one interface for it to be easier to refactor, change, and redeploy something that it has a very defined role or purpose.

D ependency Inversion
	
Entities must depend on abstractions instead of concretions. Instead of using direct references from a high-level module to a low-level module, use abstractions.
	
	````
	public interface BluetoothCapabalePhone {
    void acceptCall();
    void declineCall();
	}
	public class ApplePhone implements BluetoothCapabalePhone {
		void acceptCall(){};
		void declineCall(){};
	}
	public class SamsungPhone implements BluetoothCapabalePhone {
		void acceptCall(){};
		void declineCall(){};
	}

	public class CarHandsFree {
    BluetoothCapabalePhone phone;
    void pairWithPhone(BluetoothCapabalePhone phone){
        this.phone = phone;
    }
    void attendCall(){
        this.phone.attendCall();
    }
    void declineCall(){
        this.phone.declineCall();
    }
	}
````
	
For the above code example, we created public interface BluetoothCapabalePhone that acceptCall and declineCall. In this case either ApplePhone or SamsumgPhone or any other phone brand that is Blueetooth Capable can pair with car and attend Call or Decline Call. We will just need to implement the class BluetoothCapabalePhone in order do it so. 
	
	
	


