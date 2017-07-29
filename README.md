# utl_submit_wps64

    ```    ```
    ```   Calling WPS and WPS- PROC R from SAS  ```
    ```    ```
    ```    1.   Download and install the free WPS Express software from  ```
    ```         https://www.worldprogramming.com/us/products/wps.  ```
    ```         FYI: The express edition does not limit the size of a SAS dataset from R.  ```
    ```    ```
    ```    Execute macro utl_submit_wps64 macro (serveral methods are available)  ```
    ```    ```
    ```    1.   %utl_submit_wps64(  ```
    ```            'proc options;  ```
    ```             run;quit;');  ```
    ```    ```
    ```    2.   %let program=%str(proc options;run;quit;);  ```
    ```    ```
    ```           %utl_submit_wps64(resolve('  ```
    ```            &program  ```
    ```          '));  ```
    ```    ```
    ```    3.  %utl_submit_wps64('  ```
    ```           libname wrk sas7bdat "%sysfunc(pathname(work))";  ```
    ```           libname hlp sas7bdat "C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp";  ```
    ```           data wrk.classm;  ```
    ```              set hlp.class(where=(sex="M"));  ```
    ```           run;quit;  ```
    ```        ');  ```
    ```    ```
    ```         proc print data=classm;  ```
    ```         run;quit;  ```
    ```    ```
    ```     4.  %macro gender(sex=M);  ```
    ```           data wrk.class&sex;  ```
    ```              set hlp.class(where=(sex="&sex."));  ```
    ```           run;quit;  ```
    ```         %mend gender;  ```
    ```    ```
    ```         %utl_submit_wps64(resolve('  ```
    ```            libname wrk sas7bdat "%sysfunc(pathname(work))";  ```
    ```            libname hlp sas7bdat "C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp";  ```
    ```            %gender(sex=M);  ```
    ```            %gender(sex=F);  ```
    ```         '));  ```
    ```    ```
    ```      5.   Evaluate the character string "a**2 - 2*a*b + b**2"  ```
    ```    ```
    ```           %utl_submit_wps64('  ```
    ```             %utl_submit_wps64('  ```
    ```             libname wrk sas7bdat "%sysfunc(pathname(work))";  ```
    ```             options set=R_HOME "C:/Program Files/R/R-3.3.2";  ```
    ```             proc r;  ```
    ```             submit;  ```
    ```               a<-1;  ```
    ```               b<-2;  ```
    ```               chr="a**2 - 2*a*b + b**2";  ```
    ```               answer<-eval(parse(text = chr));  ```
    ```               answer;  ```
    ```             endsubmit;  ```
    ```             import r=answer data=wrk.answer;  ```
    ```             run;quit;  ```
    ```             ');  ```
    ```    ```
    ```             proc print data=answer;  ```
    ```             run;quit;  ```
    ```    ```
    ```      5.   Evaluate the character string "a**2 - 2*a*b + b**2"  ```
    ```    ```
    ```            options validvarname=upcase;  ```
    ```            libname sd1 "d:/sd1";  ```
    ```            data sd1.class;  ```
    ```              set sashelp.class;  ```
    ```            run;quit;  ```
    ```    ```
    ```            %utl_submit_wps64('  ```
    ```            libname sd1 sas7bdat "d:/sd1";  ```
    ```            options set=R_HOME "C:/Program Files/R/R-3.3.2";  ```
    ```            libname wrk sas7bdat "%sysfunc(pathname(work))";  ```
    ```            proc r;  ```
    ```            submit;  ```
    ```            source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);  ```
    ```            library(haven);  ```
    ```            have<-read_sas("d:/sd1/class.sas7bdat");  ```
    ```            males<-have[have$SEX=="M",];  ```
    ```            endsubmit;  ```
    ```            import r=males data=wrk.males;  ```
    ```            run;quit;  ```
    ```            ');  ```
    ```    ```
