
/*Author Nadeeshaan Gunasinghe*/
/*This code include the Dining philosopher problem*/



class chopstick 
{
	int numChopsticks;
	int max_chopsticks;

	chopstick(int InNumChopsticks)
	{
		numChopsticks=InNumChopsticks;
		max_chopsticks=InNumChopsticks;
	}

	public synchronized void get_stick(philosopher ph)
	{
		while(numChopsticks==0)
		{
			try
			{
				wait();
			}
			catch(InterruptedException ie){ }
		}
		notifyAll();
		while(numChopsticks!=0&&ph.num_of_chopsticks!=2){
		ph.num_of_chopsticks++;
		numChopsticks--;}		
	}

	public synchronized void put_stick(philosopher ph)
	{
		while(numChopsticks==max_chopsticks)
		{
			try
			{
				wait();
			}
			catch(InterruptedException ie){ }
		}		
		notifyAll();
		ph.num_of_chopsticks--;
		System.out.println(ph.ph_name+" Put down one chopstick\n");
		numChopsticks++;
	}	
}

class large_bowl
{
	public boolean lidOpen=false;
	int volume;
	large_bowl(int InVolume)
	{
		volume=InVolume;
	}

	public synchronized void get_noodle(philosopher ph)
	{
		lidOpen=true;
		while(volume==0)
		{
			try
			{
				wait();
			}
			catch(InterruptedException ie){ }
		}
		notifyAll();
		ph.filledBowl=true;	
		volume---;
		lidOpen=false;
		System.out.println(ph.ph_name+" Served himself some noodles\n");
	}
}

class philosopher implements Runnable
{
	large_bowl lBowl;
	int bowl_size=2;
	boolean filledBowl=false;
	chopstick cs1;
	String ph_name;
	int num_of_chopsticks=0;	
	
	philosopher(String InName,chopstick Incs,large_bowl InBowl)
	{
		lBowl=InBowl;
		cs1=Incs;
		ph_name=InName;

	}	

	public void take_chopstick()
	{

		if(lBowl.volume==0)
		{
			Thread.currentThread().interrupt();
			System.out.println("Bowl empty,Dinner is over");
		}

		if(num_of_chopsticks<2)
		{
			cs1.get_stick(this);
			System.out.println(ph_name+" got a chopstick\n");
			System.out.println(ph_name+" has "+ num_of_chopsticks+" chopsticks\n");
		} 
	}

	public void serve_noodles()
	{

		if(lBowl.volume==0)
		{
			Thread.currentThread().interrupt();
			System.out.println("Bowl empty,Dinner is over");
		}

		if(num_of_chopsticks==2&&filledBowl==false)
		{
			if(lBowl.lidOpen==false)
			{
				lBowl.get_noodle(this);
				while(num_of_chopsticks!=0)
				{
					cs1.put_stick(this);
				}System.out.println(this.ph_name+" Is Thinking!\n");
				try
				{
					Thread.sleep(500);
				}
				catch(InterruptedException ie){ }
			}		
		}
	}

	public void eat_noodles()
	{

		if(lBowl.volume==0)
		{
			Thread.currentThread().interrupt();
			System.out.println("Bowl empty,Dinner is over");
		}

		if(num_of_chopsticks==2&&filledBowl==true)
		{
			System.out.println(this.ph_name+" is eating some noodle!\n");
			bowl_size--;
			if(bowl_size==0)
			{
				filledBowl=false;
			}
		
			while(num_of_chopsticks!=0)
			{
				cs1.put_stick(this);
				try
				{
					Thread.sleep(500);
				}
				catch(InterruptedException ie){ }
			}
			
			System.out.println(this.ph_name+" Is Thinking!\n");

			try
			{
				Thread.sleep(500);
			}
			catch(InterruptedException ie){ }			
		}
	}
	

	public void run()
	{		
		while(lBowl.volume!=0)
		{

			take_chopstick();
			serve_noodles();
			eat_noodles();
		}	
	}
		
}



public class dPhilosopher
{
	public static void main(String[] arguments)
	{
		chopstick CHOPSTICK=new chopstick(5);
		large_bowl LARGE_BOWL=new large_bowl(6);

		philosopher ph1=new philosopher("Philosopher 1",CHOPSTICK,LARGE_BOWL);
		philosopher ph2=new philosopher("Philosopher 2",CHOPSTICK,LARGE_BOWL);
		philosopher ph3=new philosopher("Philosopher 3",CHOPSTICK,LARGE_BOWL);
		philosopher ph4=new philosopher("Philosopher 4",CHOPSTICK,LARGE_BOWL);
		philosopher ph5=new philosopher("Philosopher 5",CHOPSTICK,LARGE_BOWL);
	

		Thread thread1=new Thread(ph1);
		thread1.setPriority(3);
		thread1.start();

		Thread thread2=new Thread(ph2);
		thread2.setPriority(7);
		thread2.start();

		Thread thread3=new Thread(ph3);
		thread3.setPriority(3);
		thread3.start();

		Thread thread4=new Thread(ph4);
		thread4.setPriority(2);
		thread4.start();

		Thread thread5=new Thread(ph5);
		thread5.setPriority(4);
		thread5.start();
		
	}
}