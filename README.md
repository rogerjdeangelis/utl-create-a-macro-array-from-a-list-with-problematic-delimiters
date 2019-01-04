# utl-create-a-macro-array-from-a-list-with-problematic-delimiters
Create a macro array from a list with problematic delimiters
    Create a macro array from a list with problematic delimiters

       Prpblem

          Given
             %let a= a1, a2, a3, a4, a5;

          Create macro variables

              AN=5

              A1=a1
              A2=a2
              A3=a3
              A2=a2
              A5=a5

        Three solutions

             1. %array(a,values=%superq(a),delim=%nrstr(, ));
             2. %array(a,values=a1-a5);
             3. Datastep

    github
    https://tinyurl.com/y9rwu6ru
    https://github.com/rogerjdeangelis/utl-create-a-macro-array-from-a-list-with-problematic-delimiters

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories


    SAS Forum
    https://tinyurl.com/ydf4thtm
    https://communities.sas.com/t5/New-SAS-User/Select-from-the-first-to-the-k-th-element-in-a-macro-list/m-p/524416



    Process
    =======

     1. %array(a,values=%superq(a),delim=%nrstr(, ));

      %symdel a1 a2 a3 a4 a5 an/ nowarn;
      %let a = a1, a2, a3, a4, a5;
      %array(a,values=%superq(a),delim=%nrstr(, ));

      %utlnopts;

      %put &=an;

      %put &=a1;
      %put &=a2;
      %put &=a3;
      %put &=a2;
      %put &=a5;

      %utlopts;

      AN=5
      A1=a1
      A2=a2
      A3=a3
      A2=a2
      A5=a5


    2. %array(a,values=a1-a5);

       %symdel a1 a2 a3 a4 a5 an / nowarn;
       %let a = a1, a2, a3, a4, a5;
       %array(a,values=a1-a5);

      %utlnopts;

      %put &=an;

      %put &=a1;
      %put &=a2;
      %put &=a3;
      %put &=a2;
      %put &=a5;

      %utlopts;

    3. Datastep


       %symdel a1 a2 a3 a4 a5 an;
       %let a = a1, a2, a3, a4, a5;
       data _null_;
          str="&a";
          do idx=1 to countw(str);
             as=scan(str,idx,',');
             call symputx('a'!!put(idx,1.),as);
          end;
          call symputx('an',idx-1);
       run;quit;

      %utlnopts;

      %put &=an;

      %put &=a1;
      %put &=a2;
      %put &=a3;
      %put &=a2;
      %put &=a5;

      %utlopts;




