**Η όλη φιλοσοφία του πρώτου μέρους της HW_0 είναι η εξής**:

                        0xffff (υψηλές διευθύνσεις)
      :          
| return addr         |                                       | 
| caller's ebp        |                                       |
| callee-save         |                                       |
| stack alignment     |     -------------------------->       | 
| compiler alocations |                                       |
| architecture        |                                       |
| buffer              |                                       |
      :                  
                        0xff10 (χαμηλές διευθύνσεις)
                
