Strategy for climate control:




	Cond 0: inside <= heating (10)
		Sub 0: outside >= preemtive heating (18)
			-> fan

		Cond 0 Default:
			-> heat

	Cond 1: inside >= cooling (30)
		Sub 0: outside <= preemtive cooling (28)
			-> fan
			
		Cond 1 Default:
			-> cool

	Cond 2: inside > heating (10)
			inside < cooling (30)
			
		Sub 0: inside < preemtive heating (18)
			SubSub 0: outside > preemtive heat (18)
					  outside > inside
				-> fan
			SubSub 1: surplus >= minimum surplus heating (500)
					  surplus remaining > (minimum surplus heating (500) * change frequency (15)) / 60
				-> heat 
			SubSub 2: outside > inside
				-> fan
			Sub 0 Default:
				-> off
				
		Sub 1: inside > preemtive cooling (28) -> cooling
			SubSub 0: outside < preemtive cool (28)
					  outside < inside
				-> fan
			SubSub 1: surplus >= minimum surplus cooling (500)
					  surplus remaining > (minimum surplus cooling (500) * change frequency (15)) / 60
				-> cool
			SubSub 0: outside < inside
				-> fan
			Sub 1 Default:
				-> off

		Sub 2: inside >= preemtive heating (18)
			   inside <= preemtive cooling (28)	
			SubSub 0: forecast max >= preemtive cooling (28)
				SubSubSub 0: surplus >= minimum surplus cooling (500)
							 surplus remaining > (minimum surplus cooling (500) * change frequency (15)) / 60
					-> cool
				SubSub 0 Default:
					-> off
			
			SubSub 1: forecase max <= preemtive heating (18)
				SubSubSub 0: surplus >= minimum surplus heating (500)
							 surplus remaining > (minimum surplus heating (500) * change frequency (15)) / 60
					-> heat 
				SubSub 1 Default:
					-> off
			Sub 2 Default:
				-> off
		Cond 2 Default:
			-> off
	Default:
		-> off
