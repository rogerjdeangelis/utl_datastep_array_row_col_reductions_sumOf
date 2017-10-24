# utl_datastep_array_row_col_reductions_sumOf
Extension of the SAS sum(of to two dimensional arrays. Row and column reductions, sums, as right side clauses.

    ```  Row and column sum reductions using a datastep array                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  As Rick has shown, this type of problem is best solved with a matrix language.                                                                               ```
    ```                                                                                                                                                               ```
    ```    Two macros on end of message.                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```    Compute the difference between total truck and wagon sales                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     Given                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```         LABEL     ASIA    EUROPE    USA                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```         Hybrid      2        0        0                                                                                                                       ```
    ```         SUV        25       10       24                                                                                                                       ```
    ```         Sedan      94       70       90                                                                                                                       ```
    ```         Sports     15       22        8                                                                                                                       ```
    ```         Truck       8        0       16    ** sum=24                                                                                                          ```
    ```         Wagon      11       11        7    ** sum=29  29-24=5                                                                                                 ```
    ```                                                                                                                                                               ```
    ```      WANT                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```         Up to 40 obs WORK.WANT total obs=1                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```         Obs      DIFNAM       DIF                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```          1     Truck-Wagon     -5                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```        %Utl_MkeAry                                                                                                                                            ```
    ```          (                                                                                                                                                    ```
    ```           Utl_InDsn     = cars,                                                                                                                               ```
    ```           Utl_InRowVar  = type,                                                                                                                               ```
    ```           Utl_InColVar  = origin,                                                                                                                             ```
    ```           Utl_MacRetVar = numLst                                                                                                                              ```
    ```          );                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```        /* macro return variable contains                                                                                                                      ```
    ```        {6,3} ( 2 0 0 25 10 24 94 70 90 15 22 8 8 0 16 11 11 7 )                                                                                               ```
    ```        */                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```        data want;                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```          array mat&numLst ;                                                                                                                                   ```
    ```          difNam  = catx('-',symget('row5'),symget('row6'));                                                                                                   ```
    ```                                                                                                                                                               ```
    ```          dif    = %utlSumOf(mat,5,1:3) - %utlSumOf(mat,6,1:3);                                                                                                ```
    ```                                                                                                                                                               ```
    ```          keep difNam dif;                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```         run;quit;                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```     WORK.CARS total obs=413                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```       Obs    TYPE      ORIGIN                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```         1    SUV       Asia                                                                                                                                   ```
    ```         2    Sedan     Asia                                                                                                                                   ```
    ```         3    Sedan     Asia                                                                                                                                   ```
    ```         4    Sedan     Asia                                                                                                                                   ```
    ```         5    Sedan     Asia                                                                                                                                   ```
    ```         6    Sedan     Asia                                                                                                                                   ```
    ```         7    Sports    Asia                                                                                                                                   ```
    ```         8    Sedan     Europe                                                                                                                                 ```
    ```         9    Sedan     Europe                                                                                                                                 ```
    ```        10    Sedan     Europe                                                                                                                                 ```
    ```       ...    ...       ...                                                                                                                                    ```
    ```       409    SUV       Europe                                                                                                                                 ```
    ```       410    Sedan     Europe                                                                                                                                 ```
    ```       411    Sedan     Europe                                                                                                                                 ```
    ```       412    Sedan     Europe                                                                                                                                 ```
    ```       413    Wagon     Europe                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  WANT                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```     Up to 40 obs WORK.WANT total obs=1                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```     Obs      DIFNAM       DIF                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```      1     Truck-Wagon     -5                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  proc datasets lib=work kill;                                                                                                                                 ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  %symdel numLst row1 row2 row3 row4 row5 row6  col1 col2 col3 / nowarn;                                                                                       ```
    ```                                                                                                                                                               ```
    ```  data cars(keep=type origin);                                                                                                                                 ```
    ```    set sashelp.cars(where=(cylinders in (4,6,8)));                                                                                                            ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %Utl_MkeAry                                                                                                                                                  ```
    ```    (                                                                                                                                                          ```
    ```     Utl_InDsn     = cars,                                                                                                                                     ```
    ```     Utl_InRowVar  = type,                                                                                                                                     ```
    ```     Utl_InColVar  = origin,                                                                                                                                   ```
    ```     Utl_MacRetVar = numLst                                                                                                                                    ```
    ```    );                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  /* macro return variable contains                                                                                                                            ```
    ```  {6,3} ( 2 0 0 25 10 24 94 70 90 15 22 8 8 0 16 11 11 7 )                                                                                                     ```
    ```  */                                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  data want;                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```    array mat&numLst ;                                                                                                                                         ```
    ```    difNam  = catx('-',symget('row5'),symget('row6'));                                                                                                         ```
    ```                                                                                                                                                               ```
    ```    dif    = %utlSumOf(mat,5,1:3) - %utlSumOf(mat,6,1:3);                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    keep difNam dif;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```   run;quit;                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  /*                                                                                                                                                           ```
    ```  Limited LOG                                                                                                                                                  ```
    ```  MLOGIC(UTLSUMOF):  %DO loop index variable J is now 4; loop will not iterate again.                                                                          ```
    ```  MLOGIC(UTLSUMOF):  %DO loop index variable I is now 7; loop will not iterate again.                                                                          ```
    ```  MPRINT(UTLSUMOF):   sum ( of mat(6,1) mat(6,2) mat(6,3) )                                                                                                    ```
    ```  MLOGIC(UTLSUMOF):  Ending execution.                                                                                                                         ```
    ```  1694    keep difNam dif;                                                                                                                                     ```
    ```  1695   run;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```  NOTE: The data set WORK.WANT has 1 observations and 2 variables.                                                                                             ```
    ```  */                                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  *                                                                                                                                                            ```
    ```   _ __ ___   __ _  ___ _ __ ___  ___                                                                                                                          ```
    ```  | '_ ` _ \ / _` |/ __| '__/ _ \/ __|                                                                                                                         ```
    ```  | | | | | | (_| | (__| | | (_) \__ \                                                                                                                         ```
    ```  |_| |_| |_|\__,_|\___|_|  \___/|___/                                                                                                                         ```
    ```                        ___   __                                                                                                                               ```
    ```   ___ _   _ _ __ ___  / _ \ / _|                                                                                                                              ```
    ```  / __| | | | '_ ` _ \| | | | |_                                                                                                                               ```
    ```  \__ \ |_| | | | | | | |_| |  _|                                                                                                                              ```
    ```  |___/\__,_|_| |_| |_|\___/|_|                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %Macro UtlSumOf                                                                                                                                              ```
    ```          (                                                                                                                                                    ```
    ```           Utl_Mat,   /* Datastep Matrix */                                                                                                                    ```
    ```           Utl_Rows,  /* Range or Single row ie 2:5, 1:10, 4 */                                                                                                ```
    ```           Utl_Cols   /* Range or Single row ie 2:5, 1:10, 4 */                                                                                                ```
    ```          ) / Des="Column and Row Sum Reductions for Two Dimensional Arrays";                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  /*---------------------------------------------*\                                                                                                            ```
    ```  |  You have the following Array Statement       |                                                                                                            ```
    ```  |  Example :                                    |                                                                                                            ```
    ```  |  Array Mat{2,3} ( 1 2 3                       |                                                                                                            ```
    ```  |                   4 5 6 );                    |                                                                                                            ```
    ```  |  And you want the Row, Column and Grand Totals|                                                                                                            ```
    ```  |  Data _Null_;                                 |                                                                                                            ```
    ```  |  Array Mat{2,3} ( 1 2 3                       |                                                                                                            ```
    ```  |  ColSum1= %UtlSumOf ( Mat,1:2,1);             |                                                                                                            ```
    ```  |  ColSum2= %UtlSumOf ( Mat,1:2,2);             |                                                                                                            ```
    ```  |  ColSum3= %UtlSumOf ( Mat,1:2,3);             |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  RowSum1= %UtlSumOf ( Mat,1,1:3);             |                                                                                                            ```
    ```  |  RowSum2= %UtlSumOf ( Mat,2,1:3);             |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  Total=%UtlSumOf (Mat,1:2,1:3);               |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  Put                                          |                                                                                                            ```
    ```  |      ColSum1=  /                              |                                                                                                            ```
    ```  |      ColSum2=  /                              |                                                                                                            ```
    ```  |      ColSum3=  /                              |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |      RowSum1=  /                              |                                                                                                            ```
    ```  |      RowSum2=   ;                             |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  Run;                                         |                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  You could use the macro language  to simplify|                                                                                                            ```
    ```  |                                               |                                                                                                            ```
    ```  |  Array Colsum{3};                             |                                                                                                            ```
    ```  |  %Do Col=1 %To 3;                             |                                                                                                            ```
    ```  |    ColSum{&Col}= %UtlSumOf ( Mat,1:2,&Col );  |                                                                                                            ```
    ```  |  %End;                                        |                                                                                                            ```
    ```  \*---------------------------------------------*/                                                                                                            ```
    ```                                                                                                                                                               ```
    ```     %Local i j;                                                                                                                                               ```
    ```     %If &Utl_Mat.  = %Str() or                                                                                                                                ```
    ```         &Utl_Rows. = %Str() or                                                                                                                                ```
    ```         &Utl_Cols. = %Str()                                                                                                                                   ```
    ```     %Then %Do;                                                                                                                                                ```
    ```         %Put Error User Required Parm Missing;                                                                                                                ```
    ```         %put Utl_Mat  =   &Utl_Mat.  ;                                                                                                                        ```
    ```         %put Utl_Rows =   &Utl_Rows. ;                                                                                                                        ```
    ```         %put Utl_Cols =   &Utl_Cols. ;                                                                                                                        ```
    ```         %goto exit;                                                                                                                                           ```
    ```     %end;                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```   %If %index(&Utl_Rows.,%str(:)) Ne 0 %Then %Do;                                                                                                              ```
    ```     %Let Utl_Row1st=%qscan(&Utl_Rows.,1,%str(:));                                                                                                             ```
    ```     %Let Utl_RowLst=%qscan(&Utl_Rows.,2,%str(:));                                                                                                             ```
    ```   %end;                                                                                                                                                       ```
    ```   %else %If %index(&Utl_Rows.,%str(+)) Ne 0 %Then %Do;                                                                                                        ```
    ```   %end;                                                                                                                                                       ```
    ```   %Else %Do;                                                                                                                                                  ```
    ```     %Let Utl_Row1st=&Utl_Rows.;                                                                                                                               ```
    ```     %Let Utl_RowLst=&Utl_Rows.;                                                                                                                               ```
    ```   %End;                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```   %If %index(&Utl_Cols.,%str(:)) Ne 0 %Then %Do;                                                                                                              ```
    ```     %Let Utl_Col1st=%qscan(&Utl_Cols.,1,%str(:));                                                                                                             ```
    ```     %Let Utl_ColLst=%qscan(&Utl_Cols.,2,%str(:));                                                                                                             ```
    ```   %end;                                                                                                                                                       ```
    ```   %Else %Do;                                                                                                                                                  ```
    ```     %Let Utl_Col1st=&Utl_Cols.;                                                                                                                               ```
    ```     %Let Utl_ColLst=&Utl_Cols.;                                                                                                                               ```
    ```   %End;                                                                                                                                                       ```
    ```     sum ( of                                                                                                                                                  ```
    ```     %do i = &Utl_Row1st. %to &Utl_RowLst.;                                                                                                                    ```
    ```       %do j=&Utl_Col1st. %to &Utl_ColLst.;                                                                                                                    ```
    ```         &Utl_Mat.(&i.,&j.)                                                                                                                                    ```
    ```       %end;                                                                                                                                                   ```
    ```     %end;                                                                                                                                                     ```
    ```          )                                                                                                                                                    ```
    ```  %Exit:                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  /*                                                                                                                                                           ```
    ```  Data _Null_;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  Array Mat{2,3} ( 1 2 3                                                                                                                                       ```
    ```                   2 3 6 );                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  ColSum1= %UtlSumOf ( Mat,1:2,1);                                                                                                                             ```
    ```  ColSum2= %UtlSumOf ( Mat,1:2,2);                                                                                                                             ```
    ```  ColSum3= %UtlSumOf ( Mat,1:2,3);                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```  RowSum1= %UtlSumOf ( Mat,1,1:3);                                                                                                                             ```
    ```  RowSum2= %UtlSumOf ( Mat,2,1:3);                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```  Total=%UtlSumOf (Mat,1:2,1:3);                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  Put                                                                                                                                                          ```
    ```      ColSum1=  /                                                                                                                                              ```
    ```      ColSum2=  /                                                                                                                                              ```
    ```      ColSum3=  //                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```      RowSum1=  /                                                                                                                                              ```
    ```      RowSum2=  //                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```      Total=;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```  Run;                                                                                                                                                         ```
    ```  */                                                                                                                                                           ```
    ```  %mend UtlSumOf;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```  *          _           _                                                                                                                                     ```
    ```   _ __ ___ | | _____   / \   _ __ _   _                                                                                                                       ```
    ```  | '_ ` _ \| |/ / _ \ / _ \ | '__| | | |                                                                                                                      ```
    ```  | | | | | |   <  __// ___ \| |  | |_| |                                                                                                                      ```
    ```  |_| |_| |_|_|\_\___/_/   \_\_|   \__, |                                                                                                                      ```
    ```                                   |___/                                                                                                                       ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %macro Utl_MkeAry                                                                                                                                            ```
    ```     (                                                                                                                                                         ```
    ```      Utl_InDsn,                                                                                                                                               ```
    ```      Utl_InRowVar,                                                                                                                                            ```
    ```      Utl_InColVar,                                                                                                                                            ```
    ```      Utl_MacRetVar=Utl_MkeAry                                                                                                                                 ```
    ```     ) / Des="Create an Array Statement with Freq counts";                                                                                                     ```
    ```                                                                                                                                                               ```
    ```    Ods Exclude All;                                                                                                                                           ```
    ```    Ods Output Observed=Utl_MkeAry01;                                                                                                                          ```
    ```    Proc Corresp Data=&Utl_InDsn                                                                                                                               ```
    ```                 Observer                                                                                                                                      ```
    ```                 dim=1;                                                                                                                                        ```
    ```         Table                                                                                                                                                 ```
    ```                 &Utl_InRowVar., &Utl_InColVar.;                                                                                                               ```
    ```    Run;                                                                                                                                                       ```
    ```    Ods Select All;                                                                                                                                            ```
    ```    Proc Print Data=Utl_MkeAry01;                                                                                                                              ```
    ```    Run;                                                                                                                                                       ```
    ```    Proc Print Data=Utl_MkeAry01;                                                                                                                              ```
    ```    Run;                                                                                                                                                       ```
    ```  %Let Cols=%str();                                                                                                                                            ```
    ```  %Let Rows=%Str();                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  Data _Null_;   /* Get Number of ROws and Columns */                                                                                                          ```
    ```    Set Work.Utl_MkeAry01 Nobs=Mobs;                                                                                                                           ```
    ```    Array Cols{*} _Numeric_;                                                                                                                                   ```
    ```    Call SymPut('Rows',Compress (Put(Mobs-1,9. )));                                                                                                            ```
    ```    Call SymPut('Cols',Compress (Put(Dim(Cols)-1,5.)));                                                                                                        ```
    ```    Stop;                                                                                                                                                      ```
    ```  Run;                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  %Put Rows=&Rows;                                                                                                                                             ```
    ```  %Put Cols=&Cols;                                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```  Data _Null_;                                                                                                                                                 ```
    ```    Length MacStr $32700;                                                                                                                                      ```
    ```    Retain MacStr;                                                                                                                                             ```
    ```    Set Work.Utl_MkeAry01;                                                                                                                                     ```
    ```    Array Cols{*} _Numeric_;                                                                                                                                   ```
    ```    If _n_ =1 Then MacStr ="{&Rows.,&Cols.} ( ";                                                                                                               ```
    ```     Do J= 1 To Dim(Cols)-1;                                                                                                                                   ```
    ```      MacStr=Trim(MacStr)!!' '!!Compress(Put(Cols{J},9.));                                                                                                     ```
    ```     End;                                                                                                                                                      ```
    ```    If _n_ =&Rows. Then Do;                                                                                                                                    ```
    ```      MacStr=Trim(MacStr)!!' )';                                                                                                                               ```
    ```      /* do not change anything below this line */                                                                                                             ```
    ```      Call Symput(%UnQuote(%Bquote('&Utl_MacRetVar.')),Trim(MacStr));                                                                                          ```
    ```      Stop;                                                                                                                                                    ```
    ```    End;                                                                                                                                                       ```
    ```    run /* do not put a semicoln here */                                                                                                                       ```
    ```  %Exit:                                                                                                                                                       ```
    ```  %Mend Utl_MkeAry;                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

