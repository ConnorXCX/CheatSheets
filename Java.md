# Java Cheat Sheet

## String Manipulation

```java
char c = s.charAt(i);
```

```java
String front = s.substring(0, i);
String back = s. substring(i + 1);
s = front + "*" + back;
```

## Arrays

### Creating Arrays

```java
String[] names = new String[10];
```

### Initializing Arrays

```java
String[] names = {"One", "Two", "Three"};
```

```java
int[] primes = { 2, 3, 5, 7, 11, 13, 17 };
```

```java
int[] primes = new int[] { 2, 3, 5, 7, 11, 13, 17 };
```

_Note: The length of an array created with an initializer is determined by the number of values listed in the initializer._

### Looping thru Arrays

```java
for (int i = 0; i < players.length; i++)
    System.out.println(players[i]);
```

_Note: If you don’t have the array length handy, you can get it from the array’s_ `.length` _**property**. Recall using the_ `.length()` _**method** call for a String._

### Two-Dimensional Arrays

```java
double[][] sales = new double[5][4];
```

### Varargs

_Note: An important caveat about using_ `varargs` _is that the variable argument must always be the last argument in the argument list. This makes sense when you consider that, otherwise, the compiler wouldn’t be able to keep track of the arguments if any other than the last argument had a variable number._

**Example:**

```java
public static void PrintSomeWords(String… words)
{
    for (String word : words)
        System.out.println(word);
}
```

### Jagged Arrays

_Note: Java lets you create two-dimensional arrays in which the length of each element of the main array is different. This is sometimes called a **jagged array** because the array doesn’t form a nice rectangle. Instead, its edges are jagged._

**Example:**

```java

String[][] teams =
{
    {"Henry Blake", "Johnny Mulcahy"},
    {"Benjamin Pierce", "John McIntyre", "Jonathan Tuttle"},
    {"Margaret Houlihan", "Frank Burns"},
    {"Max Klinger", "Radar O'Reilly", "Igor Straminsky"}
};

for (String[] team : teams)
{
    for (String player : team)
        System.out.println(player);
    System.out.println();
}
```

## Loops

### `while` Loop

```java
int number = 0;

while (number < 20)
{
    number += 2;

    if (number == 12)
        continue;

    System.out.print(number + " ");
}

System.out.println();
```

### `do-while` Loop

```java
int number = 2;

do
{
    System.out.print(number + " ");
    number += 2;
} while (number <= 20);

System.out.println();
```

### `for` Loop

```java
System.out.print ("We are go for launch in T minus ");

for (int count = 10; count >= 0; count--)
{
    if (count == 8)
        System.out.println("Ignition sequence start!");
    else
        System.out.println(count + "…");
}
```

### `for-each` Loop

```java
String[] days = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };

for (String day : days)
{
    System.out.println(day);
}
```

_Note: It’s important to note that the_ `for-each` _loop gives you a copy of each item in the array, not the item itself. So, you can’t alter the contents of an array by using a_ `for-each` _loop._

## `switch` Statement

```java
System.out.println("The car wash application!\n\n");
System.out.print("Enter the package code: ");
String s = sc.next();
char p = s.charAt(0);

String details = switch (p)
{
    case 'E','e' -> packageE() + packageD() + packageC() + packageB() + packageA();
    case 'D','d' -> packageD() + packageC() + packageB() + packageA();
    case 'C','c' -> packageC() + packageB() + packageA();
    case 'B','b' -> packageB() + packageA();
    case 'A','a' -> packageA();
    default -> "That's not one of the codes.";
    };

    System.out.println("\nThat package includes:\n");
    System.out.println(details);
}

public static String packageA()
{
    return "\tWash, vacuum, and hand dry.\n";
}

public static String packageB()
{
    return "\tWax, plus … \n";
}

public static String packageC()
{
    return "\tLeather/Vinyl Treatment, plus … \n";
}

public static String packageD()
{
    return "\tTire Treatment, plus … \n";
}

public static String packageE()
{
    return "\tNew Car Scent, plus … \n";
}
```

## Dates and Times

TBD

## Variables and Data Types

TBD
