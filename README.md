Apex Coding Standard

Naming Convention
------------------

  Classes:
     As per Object Oriented Programming language rules, class names should be nouns. They should define or describe a
     thing or entity. A class name should be camel-case. The first letter of each word in the class name should be
     capitalized. The class name should be simple and descriptive. Acronyms and abbreviations should be used sparingly
     and economically to avoid confusion. Do not use underscore or other special characters in a class name.
     e.g. Account, RevenueDepartment, MinecraftVehicle

     There are a few recommended variations for different types of classes
        Batch Apex Class: The class name should be suffixed by 'Batch'.
                          e.g. AccountRefundBatch, ValidateOpportunityBatch
        Controller: The class name is typically suffixed by 'Controller'
                    e.g. SolarEnergyController, NewAccountController
        Trigger: Use trigger framework[https://bit.ly/2DX0QKb] when developing triggers, the main sObject trigger
                 name should be suffixed by 'Trigger', and the handler Class should be suffixed by 'TriggerHandler'
                 e.g. AccountTrigger, AccountTriggerHandler.
        Test Classes: A test class should be suffixed by 'Test'. e.g. DebitAccountTest, CreditAccountTest

  Interfaces:
     Interface names follow the same rules as Classes and should be prefixed with a capital I e.g. IRecipe, ICoupon.  
     Where the interface is describing the ability to be used in a certain way, the interface name should be an
     adjective and end with the suffix 'ible' or 'able' e.g. IBatchable


  Variables:
     Variable names should be mixed case with a lowercase first letter and each consecutive word starts with capital
     letters. This rule applies to instance and class variables. They should not start with an underscore(_), a
     dollar sign($), even though both are allowed. Infact you should avoid using underscores or special characters in
     a variable name. Variables names should short yet meaningful. It should indicate the intent of its use.
     Avoid single letter variable names like (i, j, k), unless they are used as a throwaway variable in a loop.

  Constants:
     Constants (i.e. variables defined as static final int), are a special type of variable and a constant name
     should be all uppercase with words seperated by underscores(_). Avoid any special characters in a constant name.
     e.g MIN_WIDTH, UK_CURRENCY

  Methods:
     Method name should be a verb, an action. Like a variable name, it should be mixed case with a lowercase first
     letter and the first letter of each internal word capitalized.

  Documents:
     You should follow the following naming proto-pattern for Documents.
     'Project Name - Title of Document - Document Order - Version'


Code Layout and Formatting
--------------------------
A well formatted code increases readability, understanding and ultimately maintainability of the code base.
A developer should strive to use a consistent layout and format. It will make the lives of other developers
(who want to read, review, or maintain your code) a lot easier. I have listed a few guidelines as to how a
Force.com developer should format code.

  == Wrapping Lines:

     When an expression will not fit on a single line, break it according to these general principles:
       * Break after a comma
       * Break before an operator
       * Prefer higher-level breaks to lower-level breaks
       * Align the new line with the beginning of the expression at the same level on the previous line.
       * If the above rules lead to confusing code or to code that's squished up against the right margin, just
         indent 8 spaces instead.

     Here are some examples of breaking method calls:

       someMethod(longExpression1, longExpression2, longExpression3,
                  longExpression4, longExpression5);
       var = someMethod1(longExpression1,
                         someMethod2(longExpression2,
                         longExpression3));

     Following are two examples of breaking an arithmetic expression.
     The first is preferred, since the break occurs outside the parenthesized expression, which is at a higher level.

        longName1 = longName2 * (longName3 + longName4 - longName5)
                    + 4 * longname6; // PREFER

        longName1 = longName2 * (longName3 + longName4
                                 - longName5) + 4 * longname6; // AVOID

     Following are two examples of indenting method declarations.
     The first is the conventional case.
     The second would shift the second and third lines to the far right if it used conventional indentation, so
     instead it indents only 8 spaces.

         //CONVENTIONAL INDENTATION
         someMethod(int anArg, Object anotherArg, String yetAnotherArg,
               Object andStillAnother) {
        ...
        }

         //INDENT 8 SPACES TO AVOID VERY DEEP INDENTS
         private static synchronized horkingLongMethodName(int anArg,
                 Object anotherArg, String yetAnotherArg,
                 Object andStillAnother) {
        ...
         }

      Line wrapping for if statements should generally use the 8-space rule, since conventional (4 space)
      indentation makes seeing the body difficult. For example:

         //DON'T USE THIS INDENTATION
         if ((condition1 && condition2)
            || (condition3 && condition4)
            ||!(condition5 && condition6)) { //BAD WRAPS
            doSomethingAboutIt();            //MAKE THIS LINE EASY TO MISS
         }

         //USE THIS INDENTATION INSTEAD
         if ((condition1 && condition2)
                 || (condition3 && condition4)
                 ||!(condition5 && condition6)) {
            doSomethingAboutIt();
         }

        //OR USE THIS
        if ((condition1 && condition2) || (condition3 && condition4)
                ||!(condition5 && condition6)) {
            doSomethingAboutIt();
        }

      Here are three acceptable ways to format ternary expressions:

         alpha = (aLongBooleanExpression) ? beta : gamma;  

         alpha = (aLongBooleanExpression) ? beta
                                          : gamma;  

         alpha = (aLongBooleanExpression)
                 ? beta
                 : gamma;  


  == Placement:

    Put declarations only at the beginning of blocks. (A block is any code surrounded by curly braces "{" and "}".)
    Don't wait to declare variables until their first use; it can confuse the unwary programmer and hamper code
    portability within the scope.

        void myMethod() {
            int int1 = 0;         // beginning of method block

            if (condition) {
                 int int2 = 0;     // beginning of "if" block
            ...
            }
        }

    The one exception to the rule is indexes of for loops, which in Java can be declared in the for statement:

        for (int i = 0; i < maxLoops; i++) { ... }

    Avoid local declarations that hide declarations at higher levels. For example, do not declare the same variable
    name in an inner block:

        int count;
    ...
        myMethod() {
            if (condition) {
                int count = 0; // AVOID!
            ...
            }
        ...
        }

  == Comments

    If you need to put comments before a class, field, constructor or method declaration to tell what they are for, use doc comment style(/** ... */)
    All apex classes should be commented with date, author, description, and
    history:

        /**
         * Date
         * Author
         * Description
         * History
         */

  == Class and Interface Declarations:

    When coding Apex classes and interfaces, the following formatting rules should be followed:
        * No space between a method name and the parenthesis "(" starting its parameter list
        * Open brace "{" appears at the end of the same line as the declaration statement
        * Closing brace "}" starts a line by itself indented to match its corresponding opening statement,
          except when it is a null statement the "}" should appear immediately after the "{"

           class Sample extends Object {
                int ivar1;
                int ivar2;

                Sample(int i, int j) {
                    ivar1 = i;
                    ivar2 = j;
                }

                int emptyMethod() {}

           }

  == if, if-else, if else-if else Statements:

    The if-else class of statements should have the following form:

        if (condition) {
            statements;
        }

        if (condition) {
            statements;
        } else {
            statements;
        }

        if (condition) {
            statements;
        } else if (condition) {
            statements;
        } else {
            statements;
        }

    Note: if statements should always use braces {}. Avoid the following error-prone form:
        if (condition) //AVOID! THIS OMITS THE BRACES {}!
            statements;

  == for Loop

    A for loop should have the following format:

        //traditional for loop
        for (initStatement; exitCondition, incrementStatement) {
            //code block
        }

        //set iteration for loop
        for (variable : list_or_set) {
            //code block
        }

        //SOQL for loop
        for (variable : [soql query]) {
            //code block
        }

    Make sure you break the query into multiple lines if it is a long query.


  == try-catch Statements:

    A try-catch statement should have the following format:

        try {
            statements;
        } catch (ExceptionClass e) {
            statements;
        }

    A try-catch statement may also be followed by finally, which executes regardless of whether or not the
    try block has completed successfully.

        try {
            statements;
        } catch (ExceptionClass e) {
            statements;
        } finally {
            statements;
        }

  == Blank Lines:

    Blank lines improve readability by setting off sections of code that are logically related.

    Two blank lines should always be used in the following circumstances:

        * Between sections of a source file
        * Between class and interface definitions

    One blank line should always be used in the following circumstances:

        * Between methods
        * Between the local variables in a method and its first statement
        * Before a block or single-line comment
        * Between logical sections inside a method to improve readability

Best Practices
--------------
These are the key coding principles and best practices that will ensure we write efficient, scalable code.

  == Keep code stupid simple:

    There should be as little logic in your code as possible. Reusing code in several places,
    should be replaced with a single method and reduce the clutter in the code base.

      //BAD EXAMPLE
      public boolean isTrue(boolean myBool){
          if(myBool){
              return true;
          }else{
              return false;
          }
      }

      public Map<Id,Contact> getContactMap(){
          Map<Id,Contact> contactMap = new Map<Id,Contact>();

          List<Contact> contacts = [Select Id From Contact];
          if(contacts != null && contacts.size() > 0 && !contacts.isEmpty()){
              for(Integer i=0; i < contacts.size(); i++){
                  contactMap.put(contacts.get(i).Id,contacts.get(i));
              }
          }
          return contactMap;
      }

      //GOOD Example
      public boolean isTrue(boolean myBool){
          return myBool;
      }

      public Map<Id,Contact> getContactMap(){
          return new Map<Id,Contact>([Select Id From Contact]);
      }

  == Do not put queries in loops:

    One of the most stringent governor limits is a SOQL query limit of 100 queries in a transaction.
    To avoid this simply do not put queries in for loops.

      //BAD example
      List<Account> accList = new List<Account>([Select Id,Name From Account]);

      for(Account acc : accList){
          Integer numWithEmail = 0;
          for(Contact cont : [Select Id,Email From Contact Where AccountId = :acc.Id]){
              if(!String.isEmpty(cont.Email)){
                  numWithEmail++;
              }
          }
      }

      //GOOD Example
      List<Account> accList = new List<Account>(
          [Select
              Id
              ,Name
              ,(Select
                    Email
                From
                    Contacts
              )
           From Account]
      );

      for(Account acc : accList){
          Integer numWithEmail = 0;
          for(Contact cont : acc.Contacts){
              if(!String.isEmpty(cont.Email)){
                  numWithEmail++;
              }
          }
      }

  == Use maps for queries:

    This is a fundamental technique and trick to use in order to make SOQL queries, DML transactions, and Apex triggers
    more efficient. You can get a Map from a list, without a For Loop. For exampe:

      Map<Id, sObject> myAwesomeMap = new Map<Id,sObject>(List of sObjects or SOQL Query);

  == Use relationships to reduce queries

    SOQL allows you to query for parent/children record information.

      List<Account> accList = new List<Account>(
          [Select
              Id
              ,Name
              ,(Select
                    Email
                From
                    Contacts
              )
           From Account]
      );

      List<Account> accountsToUpdate = new List<Account>();
      for(Account acc : accList){
          Integer numWithEmail = 0;
          for(Contact cont : acc.Contacts){
              if(!String.isEmpty(cont.Email)){
                  numWithEmail++;
              }
          }
          acc.Contacts_With_Email_Address__c = numWithEmail;
          accountsToUpdate.add(acc);
      }
      update accountsToUpdate;

  == Do not put DML in loops:

    DML means any insert, update, delete, undelete, merge, convertLead transaction. To avoid governor limits
    simply by not putting DML in for loops, and generally speaking, make sure you're acting on multiple records.

  == Only use one trigger per object:

    Having multiple triggers across the same object greatly increases the complexity of your Salesforce org.
    By consolidating any triggers, you are less prone to mistakes, and business processes are easier to maintain.

  == Keep logic outside of triggers:

    Triggers should only contain a handful of lines of code, used for calling methods. The trigger should be used
    for managing execution order, and delegate all else to a separate Apex class such as a trigger helper.

  == Have a happy balance between clicks and code:

    Knowing when to use declarative features rather than jumping straight into an Apex or Visualforce solution
    will greatly help reduce the complexity of the code base, and improve performance and maintenance.

  == Write test code:

    You should always aim for 100% code coverage. The goal is get as high a code coverage as is sensible.

  == Avoid hardcoding IDs:

    It is paramount to avoid hardcoding IDs in the Apex code. By ensuring no IDs are stored in the Apex code,
    you are making the code much more dynamic and flexible, allowing for safe deployments between environments.
