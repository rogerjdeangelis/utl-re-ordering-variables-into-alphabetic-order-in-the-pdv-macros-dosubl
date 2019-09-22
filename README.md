# utl-reodering-variables-into-alphabetic-order-in-the-pdv-macros-dosubl
Re-odering variables into alphabetic order in the pdv macros dosubl 
    Re-ordering variables into alphabetic order in the pdv macros dosubl                                              
                                                                                                                      
    DOSUBL and the macro processor are made for meta programming                                                      
                                                                                                                      
    github                                                                                                            
    https://tinyurl.com/y26uk94u                                                                                      
    https://github.com/rogerjdeangelis/utl-re-ordering-variables-into-alphabetic-order-in-the-pdv-macros-dosubl       
                                                                                                                      
                                                                                                                      
    SAS Forum                                                                                                         
    https://tinyurl.com/y2qofhmr                                                                                      
    https://communities.sas.com/t5/SAS-Programming/sorting-all-variables-alphabetically/m-p/590469                    
                                                                                                                      
    macros                                                                                                            
    https://tinyurl.com/y9nfugth                                                                                      
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                        
                                                                                                                      
    *_                   _                                                                                            
    (_)_ __  _ __  _   _| |_                                                                                          
    | | '_ \| '_ \| | | | __|                                                                                         
    | | | | | |_) | |_| | |_                                                                                          
    |_|_| |_| .__/ \__,_|\__|                                                                                         
            |_|                                                                                                       
    ;                                                                                                                 
    data have;                                                                                                        
     input A B D F G I M Z C N L;                                                                                     
     datalines;                                                                                                       
     2 3 7 5 4 8 5 8 6 4 2                                                                                            
     2 4 1 4 2 5 6 8 0 7 5                                                                                            
     7 5 3 8 9 2 1 4 7 9 6                                                                                            
    ;                                                                                                                 
    run;                                                                                                              
                                                                                                                      
     WORK.HAVE total obs=3                                                                                            
                                                                                                                      
      A    B    D    F    G    I    M    Z    C    N    L                                                             
                                                                                                                      
      2    3    7    5    4    8    5    8    6    4    2                                                             
      2    4    1    4    2    5    6    8    0    7    5                                                             
      7    5    3    8    9    2    1    4    7    9    6                                                             
                                                                                                                      
    *            _               _                                                                                    
      ___  _   _| |_ _ __  _   _| |_                                                                                  
     / _ \| | | | __| '_ \| | | | __|                                                                                 
    | (_) | |_| | |_| |_) | |_| | |_                                                                                  
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                 
                    |_|                                                                                               
    ;                                                                                                                 
                                                                                                                      
     WORK.WANT total obs=3                                                                                            
                                                                                                                      
      A    B    C    D    F    G    I    L    M    N    Z                                                             
                                                                                                                      
      2    3    6    7    5    4    8    2    5    4    8                                                             
      2    4    0    1    4    2    5    5    6    7    8                                                             
      7    5    7    3    8    9    2    6    1    9    4                                                             
                                                                                                                      
     *                                                                                                                
     _ __  _ __ ___   ___ ___  ___ ___                                                                                
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                               
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                               
    | .__/|_|  \___/ \___\___||___/___/                                                                               
    |_|                                                                                                               
    ;                                                                                                                 
                                                                                                                      
    FYI: You may have to change the quoting in the utility macros to eliminate single quotes?                         
                                                                                                                      
    data have;                                                                                                        
     input A B D F G I M Z C N L;                                                                                     
     datalines;                                                                                                       
     2 3 7 5 4 8 5 8 6 4 2                                                                                            
     2 4 1 4 2 5 6 8 0 7 5                                                                                            
     7 5 3 8 9 2 1 4 7 9 6                                                                                            
    ;                                                                                                                 
    run;quit;                                                                                                         
                                                                                                                      
    %symdel varsn lst / nowarn;                                                                                       
    data want;                                                                                                        
        if _n_=0 then do; %let rc=%sysfunc(dosubl('                                                                   
            %array(vars,values=%varlist(have));                                                                       
            data havPre;                                                                                              
                 array vars[&varsn] $32 v1-v&varsn (%do_over(vars,phrase="?",between=comma));                         
                 call sortc(of vars[*]);                                                                              
                 call symputx("lst",catx(" ",of vars[*]));                                                            
            run;quit;                                                                                                 
            '));                                                                                                      
            retain &lst;;                                                                                             
        end;                                                                                                          
                                                                                                                      
        set have;                                                                                                     
                                                                                                                      
    run;quit;                                                                                                         
                                                                                                                      
                                                                                                                      
                                                                                                                      
