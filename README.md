# Turing-Machine-Project-
This Java program implements a Turing Machine simulator.
This Java program is an implementation of a Turing Machine simulator. The Turing Machine is a theoretical computing model that consists of a set of states, an alphabet, a set of machine alphabets, a transition table, and a tape with a head that can read and write symbols. The program allows the user to define the characteristics of the Turing Machine, such as the number of states, alphabet, machine alphabet, and transition rules.

## Here's a brief overview of the main functionalities:

### 1. Input Configuration:

* User input for the number of states, alphabet, and machine alphabet.
* User input to define the states, alphabet symbols, and machine alphabet symbols.

### 2. Transition Table Configuration:

* User input to configure the transition table for the Turing Machine.
* The transition table defines the behavior of the machine based on the current state, current input symbol, and the action to be taken (e.g., moving the head left or right, writing a symbol).

### 3. String Testing:

* Allows the user to input a string to be processed by the Turing Machine.
* The program simulates the operation of the Turing Machine on the input string using the configured transition table.
* It outputs whether the string is accepted or rejected and displays the resulting tape after the machine operation.

### 4. Utility Functions:

* Various utility functions to check the validity of inputs, such as checking if an alphabet symbol is valid, if an action is valid, if a state is valid, etc.
* The program continues to prompt the user for additional strings to test until the user chooses to exit.

Note: The program assumes that the input strings and transition rules are based on a specific alphabet, and it provides feedback on whether the strings are accepted or rejected by the simulated Turing Machine.

# code 

    import java.util.Scanner;

    public class Turing Machine Project  {
    static int NumberStates/*number of states*/, NumberAlphabets/*number of alphabet*/, NumberMachineAlphabet/*number of machine alphabet*/, HeadPointer/*Head pointer*/;
    static char[] ArrayStates, ArrayAlphabet, ArrayMachineAlphabet;/*Arrays for State & alphabet & Machine alphabet */
    static char[][] TransitionTable;/*Table of Transition*/
    static String Word;   /*String of input*/

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        boolean Flag; //boolean to check of Exceptions
        do {
            Flag = false;
            try {//check java.util.InputMismatchException ( Check the user enter int value )
                Scanner SC1 = new Scanner(System.in);
                System.out.print("1. Enter Number of States : ");
                NumberStates = SC1.nextInt();
                if (NumberStates < 1) {
                    System.out.println("Please Enter Valid Number of States\"No.>=1\"\n");
                }
            } catch (java.util.InputMismatchException e) {
                System.out.println("You Must Enter Integer Value\n");
                Flag = true; //if found Exception variable Flag = true for check if found Exception or not
            }
        } while (NumberStates < 1 || Flag);// if number of state<=0 or Found Exception return take valid value from user
        ArrayStates = new char[NumberStates]; // Array of States
        if (NumberStates != 1) { // if Number of State greater than 1 print following massages
            System.out.println("The States Named from 0 to " + (NumberStates - 1));
            System.out.println("The '0' state is Start state\n"); // set state 0 is start state
            for (int StateCounter = 0; StateCounter < NumberStates; StateCounter++) {//to store value of states in array
                char State = Integer.toString(StateCounter).charAt(0); // to convert int value as char ( 5 ~>'5' )
                ArrayStates[StateCounter] = State;
            }
        } else {// Number of state = 1
            System.out.println("The State Named 0");
            System.out.println("The '0' state is Start state\n");
            ArrayStates[0] = '0';
        }
        do {
            Flag = false; // reset Flag = false to another check
            try {
                Scanner SC2 = new Scanner(System.in);
                System.out.print("2. Enter Number of String alphabet : ");
                NumberAlphabets = SC2.nextInt();
                if (NumberAlphabets <= 0) {
                    System.out.println("Please Enter Valid Number of alphabet \"No.>=1\"\n");
                }
            } catch (java.util.InputMismatchException e) {
                System.out.println("You Must Enter Integer Value\n");
                Flag = true;
            }
        } while (NumberAlphabets <= 0 || Flag);
        ArrayAlphabet = new char[NumberAlphabets];// Array of Alphabet
        int AlphabetCounter;
        do {
            Flag = false; // reset Flag = false to another check
            for (AlphabetCounter = 0; AlphabetCounter < NumberAlphabets; AlphabetCounter++) {// to full ArrayAlphabet
                System.out.print("Enter alphabet number " + (AlphabetCounter + 1) + " : ");
                ArrayAlphabet[AlphabetCounter] = (sc.next()).charAt(0);
                if (!Character.isLetter(ArrayAlphabet[AlphabetCounter])) {// Check if user enter Alphabet as letter or not
                    System.out.println("Not Valid Alphabet\n");
                    Flag = true; // if Flag become true that means the user enter not valid alphabet
                    break;
                }
            }
            if (!Flag) { // if enter all alphabet valid print the alphabets
                System.out.print("The Character of Touring Machine : [ ");
                for (AlphabetCounter = 0; AlphabetCounter < NumberAlphabets; AlphabetCounter++) {
                    System.out.print(ArrayAlphabet[AlphabetCounter] + " ");
                }
                System.out.print("]\n\n");
            }
            if (AlphabetCounter == NumberAlphabets) { // When exiting the for, the value of "AlphabetCounter" = NumberAlphabets ~> ArrayAlphabet[NumberAlphabets] ~> error
                break; // exit from d while loop
            }
        } while (!Character.isLetter (ArrayAlphabet[AlphabetCounter]));
        do {
            try {
                Scanner SC3 = new Scanner(System.in);
                Flag = false; // reset Flag = false to another check
                System.out.print("3. Enter number of machine alphabet : ");
                NumberMachineAlphabet = SC3.nextInt();
                if (NumberMachineAlphabet <= 0) {
                    System.out.println("Please Enter Valid Number of machine alphabet \"No.>=1\"\n");
                }
            } catch (java.util.InputMismatchException e) {
                System.out.println("You Must Enter Integer Value\n");
                Flag = true;
            }
        } while (NumberMachineAlphabet <= 0 || Flag);
        ArrayMachineAlphabet = new char[NumberMachineAlphabet];// Array of machine alphabet
        for (int MachineAlphabetCounter = 0; MachineAlphabetCounter < NumberMachineAlphabet; MachineAlphabetCounter++) { // for loop to full ArrayMachineAlphabet
            System.out.print("Enter machine alphabet number " + (MachineAlphabetCounter + 1) + " : ");
            ArrayMachineAlphabet[MachineAlphabetCounter] = (sc.next()).charAt(0);
        }
        System.out.println("\n4. Transition");
        System.out.print("for each state from : ( ");
        for (int PrintStateCounter = 0; PrintStateCounter < NumberStates; PrintStateCounter++) {
            System.out.print(ArrayStates[PrintStateCounter] + " ");
        }
        System.out.print(")\n");
        System.out.print("Found transition with all alphabet : ( ");
        for (int PrintAlphabetCounter = 0; PrintAlphabetCounter < NumberAlphabets; PrintAlphabetCounter++) {
            System.out.print(ArrayAlphabet[PrintAlphabetCounter] + " ");
        }
        for (int PrintMachineAlphabetCounter = 0; PrintMachineAlphabetCounter < NumberMachineAlphabet; PrintMachineAlphabetCounter++) {
            System.out.print(ArrayMachineAlphabet[PrintMachineAlphabetCounter] + " ");
        }
        System.out.print(")\n");
        System.out.println("Number of Transition = " + (NumberAlphabets + NumberMachineAlphabet) * NumberStates/*Print Number of all alphabet in machine */ + "\n");
        TransitionTable = new char[(NumberAlphabets + NumberMachineAlphabet) * NumberStates][5]; //Table of transitions
        for (int row = 0; row < TransitionTable.length; row++) { // double for loop to full Table of transition
            System.out.println("Form of transition");
            System.out.println("(1.current state,2.current input \"symbol in head\")(3.new state,4.new symbol written,5.Action)");
            System.out.println("Enter information of Transition number " + (row + 1) + " : ");
            for (int column = 0; column < 5; column++) {
                char Input;
                int IntInput;
                if (column == 0) {
                    do {
                        System.out.print("1.current state : ");
                        Input = (sc.next()).charAt(0); // first char from Input of user //char value
                        IntInput = Input - '0';//convert char to int value
                        if (IsNotState(IntInput)) {
                            System.out.println("*****Your current state not valid*****");
                        } else { // if valid state add it in transition table
                            TransitionTable[row][column] = Input;
                        }
                    } while (IsNotState(IntInput));

                } else if (column == 1) {
                    do {
                        System.out.print("2.current Input \"symbol in head\" : ");
                        Input = (sc.next()).charAt(0); // first char from Input of user //char value
                        if (ISNotAlphabet(Input)) {
                            System.out.println("*****Your alphabet not valid*****");
                        } else { // if valid input add it to transition table
                            TransitionTable[row][column] = Input;
                        }
                    } while (ISNotAlphabet(Input));
                } else if (column == 2) {
                    do {
                        System.out.print("3.new state : ");
                        Input = (sc.next()).charAt(0); // first char from Input of user //char value
                        IntInput = Input - '0';//convert char to int value
                        if (IsNotState(IntInput)) {
                            System.out.println("*****Your new state not valid*****");
                        } else { // if valid state add it in transition table
                            TransitionTable[row][column] = Input;
                        }
                    } while (IsNotState(IntInput));
                } else if (column == 3) {
                    do {
                        System.out.print("4.new symbol written : ");
                        Input = (sc.next()).charAt(0); // first char from Input of user //char value
                        if (ISNotAlphabet(Input)) {
                            System.out.println("*****Your alphabet you want to write it not valid*****");
                        } else {// if valid input add it to transition table
                            TransitionTable[row][column] = Input;
                        }
                    } while (ISNotAlphabet(Input));
                } else { // column = 4
                    do {
                        System.out.print("5.Action (\"R,L,Y,N\") : ");
                        Input = (sc.next()).charAt(0); // first char from Input of user //char value
                        if (ISNotAction(Input)) {
                            System.out.println("*****Your Action not valid*****");
                        } else {// if valid Action add it to transition table
                            TransitionTable[row][column] = Input;
                        }
                    } while (ISNotAction(Input));
                }
            }// end of Adding in Transition table
            System.out.print("\nTransition Number " + (row + 1) + " : [ ");// print the transition state by state after full any row in Transition table
            for (int Statement = 0; Statement < 5; Statement++) {
                if (Statement < 4) {
                    System.out.print(TransitionTable[row][Statement] + " - ");
                } else {
                    System.out.print(TransitionTable[row][Statement] + " ");
                }
            }
            System.out.print("]\n");
        }// end of Adding in Transition table
        int Choice = 0;
        do { // for Check many Strings with same Transition table Not one String
            do { // for choice correct choice
                Flag = false;
                try {
                    Scanner SC4 = new Scanner(System.in);
                    System.out.println("\n1. Test String\n2. Exit");
                    System.out.print("Choice : ");
                    Choice = SC4.nextInt();
                } catch (java.util.InputMismatchException e) {
                    System.out.println("You Must Enter Integer Value(1 or 2)\n");
                    Flag = true;
                }
            } while (Flag);
            switch (Choice) {
                case 1: // test the String
                    do {
                        System.out.print("6. Enter the String : ");
                        Word = sc.next();
                        Word = Hashing(Word); // method to add 10 hash for end of string
                        if (NotValidWord(Word)) {
                            System.out.println("Not Valid Word \"Has character not valid in character's language\"");
                        }
                    } while (NotValidWord(Word));

                    do {
                        System.out.print("7. Enter initial position of head : ");
                        HeadPointer = sc.nextInt();
                        if (NotValidPosition(HeadPointer)) {
                            System.out.println("*****Not Valid Position*****");
                        }
                    } while (NotValidPosition(HeadPointer));
                    char CurrentAlphabetInHeader;
                    char CurrentState = '0'; // 0 as Start state
                    char WriteSymbol = ' ';
                    char Action = ' ';
                    int Row;
                    do {
                        for (Row = 0; Row < TransitionTable.length; Row++) { //search the transition statement of CurrentState & CurrentAlphabetInHeader
                            CurrentAlphabetInHeader = Word.charAt(HeadPointer);
                            if (TransitionTable[Row][0/*column of CurrentState*/] == CurrentState && TransitionTable[Row][1/*column of CurrentAlphabetInHeader*/] == CurrentAlphabetInHeader) {
                                CurrentState = TransitionTable[Row][2/*column of New State*/];
                                WriteSymbol = TransitionTable[Row][3/*column of WriteSymbol*/];
                                Action = TransitionTable[Row][4/*column of Actions*/];
                                break; // until it arrives and save information exit form for loop
                            }
                        }
                        Word = Write(Word, WriteSymbol, HeadPointer);//method Write Replace a character at HeadPointer in a String
                        if (Action == 'R' || Action == 'r') { //shift HeadPointer right
                            HeadPointer++;
                        }
                        if (Action == 'L' || Action == 'l') { // shift HeadPointer left
                            HeadPointer--;
                        }
                        if (Action == 'Y' || Action == 'y') { // Accept String
                            System.out.println("Accept String");
                        }
                        if (Action == 'n' || Action == 'N') { // reject String
                            System.out.println("Reject String");
                        }

                    } while (Action == 'R' || Action == 'r' || Action == 'L' || Action == 'l'); // stop if Action = Y or N
                    System.out.println("\nThe output of String : " + Word);// print new String
                    System.out.println("The Header in index : " + HeadPointer) ;// Print Position of HeadPointer
                    break;
                case 2: // case Exit
                    System.out.println("Thanks for Testing.");
                    break;
                default:
                    System.out.println("Choice 1 or 0");
            }
        } while (Choice != 2);
    }

    public static boolean ISNotAlphabet(char t) { // check the alphabet in alphabet of language or not
        for (int c1 = 0; c1 < (NumberAlphabets); c1++) {
            if (t == ArrayAlphabet[c1]) {
                return false;
            }
        }
        for (int c2 = 0; c2 < (NumberMachineAlphabet); c2++) {
            if (t == ArrayMachineAlphabet[c2]) {
                return false;
            }
        }
        return true;
    }

    public static boolean ISNotAction(char ActionChar) {// check the Action in alphabet of language or not
        return ActionChar != 'r' && ActionChar != 'R' && ActionChar != 'l' && ActionChar != 'L' && ActionChar != 'y' && ActionChar != 'Y' && ActionChar != 'n' && ActionChar != 'N';
    }

    public static boolean IsNotState(int STATE) { // check the state in State of language or not
        return STATE < 0 || STATE >= NumberStates;
    }

    public static boolean NotValidPosition(int Position) { // check the HeadPointer in alphabet of the String or not
        return Position < 0 || Position >= Word.length();
    }

    public static boolean NotValidWord(String Word) { // check the String from alphabet of language or not
        for (int i = 0; i < Word.length(); i++) {
            if (ISNotAlphabet(Word.charAt(i))) {
                return true;
            }
        }
        return false;
    }

    public static String Write(String old, char ch, int index) { // write new character in HeadPointer
        return (old.substring(0, (index)) + ch + old.substring(index + 1));
    }

    public static String Hashing(String BeforeHash) { // add hash in the end of String
        return (BeforeHash + "##########");
    }
}
