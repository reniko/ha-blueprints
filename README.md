Strategy for climate control:



	Cond 0: inside <= heating (10) 
		-> heating needed
  
  		Cond 0 - Sub 0: outside >= preemtive heating (18)
			-> fan
		Cond 0 - Default:
			-> heat

	Cond 1: inside >= cooling (30) 
		-> cooling needed
  
		Cond 1 - Sub 0: outside <= preemtive cooling (28)
			-> fan
		Cond 1 - Default:
			-> cool

	Cond 2: inside > heating (10) 
 		inside < cooling (30) 
		-> preemtive?		
  
		Cond 2 - Sub 0: inside < preemtive heating (18) 
			-> heating?
   
			Cond 2 - Sub 0 - Sub 0: outside > preemtive heat (18)
				  		outside > inside
				-> fan
    
			Cond 2 - Sub 0 - Sub 1: surplus >= minimum surplus heating (500)
				  		surplus remaining > (minimum surplus heating (500) * change frequency (15)) / 60
				-> heat 
    
			Cond 2 - Sub 0 - Sub 2: outside > inside
				-> fan
    
			Cond 2 - Sub 0 - Default:
				-> off
				
		Cond 2 - Sub 1: inside > preemtive cooling (28) 
  			-> cooling?
     
			Cond 2 - Sub 1 - Sub 0: outside < preemtive cool (28)
				  		outside < inside
				-> fan
    
			Cond 2 - Sub 1 - Sub 1: surplus >= minimum surplus cooling (500)
				  		surplus remaining > (minimum surplus cooling (500) * change frequency (15)) / 60
				-> cool
    
			Cond 2 - Sub 1 - Sub 2: outside < inside
				-> fan
    
			Cond 2 - Sub 1 - Default:
				-> off

		Cond 2 - Sub 2: inside >= preemtive heating (18)
			   	inside <= preemtive cooling (28)
       			-> optimal range reached, but check if preemtive useful because of forecase
	  
			Cond 2 - Sub 2 - Sub 0: forecast max >= preemtive cooling (28)
   				-> cooling?
       
				Cond 2 - Sub 2 - Sub 0 - Sub 0: surplus >= minimum surplus cooling (500)
							 	surplus remaining > (minimum surplus cooling (500) * change frequency (15)) / 60
					-> cool
     
				Cond 2 - Sub 2 - Sub 0 - Default:
					-> off
			
			Cond 2 - Sub 2 - Sub 1: forecase max <= preemtive heating (18)
   				-> heating?
       
				Cond 2 - Sub 2 - Sub 1 - Sub 0: surplus >= minimum surplus heating (500)
							 	surplus remaining > (minimum surplus heating (500) * change frequency (15)) / 60
					-> heat
     
				Cond 2 - Sub 2 - Sub - Default:
					-> off
     
			Cond 2 - Sub 2 - Default:
				-> off
    
		Cond 2 - Default:
			-> off
   
	Default:
		-> off
