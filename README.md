# utl-the-four-types-of-empty-sas-tables
The Four types of empty sas tables.
    The Four types of empty sas tables                                                  
                                                                                        
    github                                                                              
    https://github.com/rogerjdeangelis/utl-the-four-types-of-empty-sas-tables           
                                                                                        
    They have different properties and can be useful.                                   
                                                                                        
    I keep these around in sasuser.                                                     
                                                                                        
     TYPES OF MISSING TABLEs                                                            
                                                                                        
       1. Completely Empty                                                              
                                                                                        
          Observations          0                                                       
          Variables             0                                                       
          Indexes               0                                                       
          Observation Length    0                                                       
          Deleted Observations  0                                                       
                                                                                        
       2. Completely Empty except one deleted observation more useful                   
          Works in SQL and datastep - allows processing without error                   
                                                                                        
          Observations          0                                                       
          Variables             1                                                       
          Indexes               0                                                       
          Observation Length    8                                                       
          Deleted Observations  1                                                       
                                                                                        
       3. 1 observation 0 variables                                                     
                                                                                        
          Observations          1                                                       
          Variables             0                                                       
          Indexes               0                                                       
          Observation Length    0                                                       
          Deleted Observations  0                                                       
                                                                                        
       4. 1 observation 1 variable with missing value                                   
                                                                                        
          Observations          1                                                       
          Variables             1                                                       
          Indexes               0                                                       
          Observation Length    8                                                       
          Deleted Observations  0   
          
       5. Exists but has 0 filesize                           
                                                          
          d:/sd1/zroFylSiz.sas7bdat                           
                                                          
          Name                Date         Type        Size   
          zroFylSiz.sas7bdat   6/22/2019    sas7bdat     0     

                                                                                        
                                                                                        
    PROCESS                                                                             
    =======                                                                             
                                                                                        
    1. Completely Empty                                                                 
    -------------------                                                                 
                                                                                        
       data empty_0_obs_0_variables;                                                    
       stop;                                                                            
       run;quit;            
       
       data empty_0_obs_0_variables;                                                    
         set _null_;                                                                           
       run;quit;            
                                                                                        
                                                                                        
    2. Completely Empty except one deleted observation more useful                      
    --------------------------------------------------------------                      
                                                                                        
       data empty_0_obs_1_deleted;                                                      
        retain empty .;                                                                 
        output;                                                                         
       run;quit;                                                                        
                                                                                        
       data empty_0_obs_1_deleted ;                                                     
         modify empty_0_obs_1_deleted                                                   
                empty_0_obs_1_deleted ;                                                 
         by empty;                                                                      
         remove;                                                                        
       run;quit;                                                                        
                                                                                        
    3. 1 observation 0 variables                                                        
    ----------------------------                                                        
                                                                                        
       data empty_1_ob_0_variables(drop=empty);                                         
       retain empty .;                                                                  
       run;quit;                                                                        
                                                                                        
    4. 1 observation 1 variable with missing value                                      
    ==============================================                                      
                                                                                        
       data empty_1_ob_1_variables;                                                     
       retain empty .;                                                                  
       output;                                                                          
       run;quit;                                                                        
                                                                                        
    * if you want to keep these;                                                        
                                                                                        
    proc copy in=work out=sasuser;                                                      
     select empty: ;                                                                    
    run;quit;                                                                           
                                                                                        
