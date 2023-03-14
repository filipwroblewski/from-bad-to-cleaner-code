# from-bad-to-cleaner-code
👨‍💻🔜😊 Showing process of changeing code from bad  to cleaner one

___

## Dezinformacja i zbedne informacje

_Komentarze_

```c#
// NIE ZMIENIAC!!! 
// Najwazniejsza linijka w aplikacji - realizuje calosc dzialania systemu
Console.WriteLine("Kalkulator");

// Przypisanie zmiennych
int a, b, c = 0;
string d;

start:
    // Podanie danych
    Console.WriteLine("Podaj pierwsza liczbe:");
    a = Convert.ToInt32(Console.ReadLine());

    // Podanie danych
    Console.WriteLine("Podaj druga liczbe:");
    b = Convert.ToInt32(Console.ReadLine());

    // Podanie danych
    Console.WriteLine("Podaj operacje, ktora chcesz wykonac (+, -, *, /):");
    d = Console.ReadLine();

    // Switch
    switch (d)
    {
        case "+":
            c = a + b;
            break;
        case "-":
            c = a - b;
            break;
        case "*":
            c = a * b;
            break;
        case "/":
            if (b == 0)
            {
                Console.WriteLine("Error: Nie można dzielić przez zero.");
                goto start;
            }
            else
            {
                c = a / b;
            }
            break;
        default:
            Console.WriteLine("Error: Niepoprawna operacja.");
            goto start;
    }

    // Wynik
    Console.WriteLine("Wynik to: " + c);

    Console.WriteLine("Czy chcesz ponownie wykonac dzialanie? (t/n)");
    string choice = Console.ReadLine();

    if (choice == "t")
    {
        goto start;
    }
```

## Ukryte intencje

_int a, b, c = 0;
string d;_

```c#
Console.WriteLine("Kalkulator");

int a, b, c = 0;
string d;

start:
    Console.WriteLine("Podaj pierwsza liczbe:");
    a = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj druga liczbe:");
    b = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj operacje, ktora chcesz wykonac (+, -, *, /):");
    d = Console.ReadLine();

    switch (d)
    {
        case "+":
            c = a + b;
            break;
        case "-":
            c = a - b;
            break;
        case "*":
            c = a * b;
            break;
        case "/":
            if (b == 0)
            {
                Console.WriteLine("Error: Nie można dzielić przez zero.");
                goto start;
            }
            else
            {
                c = a / b;
            }
            break;
        default:
            Console.WriteLine("Error: Niepoprawna operacja.");
            goto start;
    }

    Console.WriteLine("Wynik to: " + c);

    Console.WriteLine("Czy chcesz ponownie wykonac dzialanie? (t/n)");
    string choice = Console.ReadLine();

    if (choice == "t")
    {
        goto start;
    }
```

## Zmiana goto

_**goto** zmienione na **do while**_

```c#
Console.WriteLine("Kalkulator");

int num1, num2, result = 0;
string operation, choice = "";

do
{
    Console.WriteLine("Podaj pierwsza liczbe:");
    num1 = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj druga liczbe:");
    num2 = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj operacje, ktora chcesz wykonac (+, -, *, /):");
    operation = Console.ReadLine();

    switch (operation)
    {
        case "+":
            result = num1 + num2;
            break;
        case "-":
            result = num1 - num2;
            break;
        case "*":
            result = num1 * num2;
            break;
        case "/":
            if (num2 == 0)
            {
                Console.WriteLine("Error: Nie można dzielić przez zero.");
                continue;
            }
            else
            {
                result = num1 / num2;
            }
            break;
        default:
            Console.WriteLine("Error: Niepoprawna operacja.");
            continue;
    }
    Console.WriteLine("The result is: " + result);

    Console.WriteLine("Czy chcesz ponownie wykonac dzialanie? (t/n)");
    choice = Console.ReadLine();
    
} while (choice == "t");
```

## Zmiana goto

_**goto** zmienione na **do while**_

```c#
Console.WriteLine("Kalkulator");

int num1, num2, result = 0;
string operation, choice = "";

do
{
    Console.WriteLine("Podaj pierwsza liczbe:");
    num1 = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj druga liczbe:");
    num2 = Convert.ToInt32(Console.ReadLine());

    Console.WriteLine("Podaj operacje, ktora chcesz wykonac (+, -, *, /):");
    operation = Console.ReadLine();

    switch (operation)
    {
        case "+":
            result = num1 + num2;
            break;
        case "-":
            result = num1 - num2;
            break;
        case "*":
            result = num1 * num2;
            break;
        case "/":
            if (num2 == 0)
            {
                Console.WriteLine("Error: Nie można dzielić przez zero.");
                continue;
            }
            else
            {
                result = num1 / num2;
            }
            break;
        default:
            Console.WriteLine("Error: Niepoprawna operacja.");
            continue;
    }
    Console.WriteLine("The result is: " + result);

    Console.WriteLine("Czy chcesz ponownie wykonac dzialanie? (t/n)");
    choice = Console.ReadLine();
    
} while (choice == "t");
```

## Funkcje do wprowadzania liczb

_utworzenie **inputNumber()** i **inputChars()**_

```c#
int inputNumber(string message)
{
    Console.WriteLine(message);
    while (true)
    {
        try
        {
            string? input = Console.ReadLine();
            int number = Convert.ToInt32(input);
            return number;
        }
        catch (FormatException)
        {
            Console.WriteLine("Bledne dane. Wprowadz liczbe calkowita.");
        }
    }
}

char inputChars(string message, string validChars)
{
    Console.WriteLine(message);
    while (true)
    {
        string? input = Console.ReadLine();
        if (input != null && input.Length == 1 && validChars.Contains(input[0]))
        {
            return input[0];
        }
        else
        {
            Console.WriteLine($"Bledne dane. Mozesz podac jedynie: {validChars}.");
        }
    }
}


Console.WriteLine("Kalkulator");

int num1, num2, result = 0;
char operation, choice = 't';

do
{
    num1 = inputNumber("Podaj pierwsza liczbe:");
    num2 = inputNumber("Podaj druga liczbe:");

    operation = inputChars("Podaj operacje, ktora chcesz wykonac (+, -, *, /):", "+-*/");

    switch (operation)
    {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 == 0)
            {
                Console.WriteLine("Error: Nie można dzielić przez zero.");
                continue;
            }
            else
            {
                result = num1 / num2;
            }
            break;
    }
    Console.WriteLine("The result is: " + result);
    choice = inputChars("Czy chcesz ponownie wykonac dzialanie? (t/n)", "tn");
    
} while (choice == 't');
```

## Funkcje do obslugi wykonywania dzialan

_utworzenie **add()**, **subtract()**, **multiply()**, **divide()**_

```c#
int inputNumber(string message)
{
    Console.WriteLine(message);
    while (true)
    {
        try
        {
            string? input = Console.ReadLine();
            int number = Convert.ToInt32(input);
            return number;
        }
        catch (FormatException)
        {
            Console.WriteLine("Bledne dane. Wprowadz liczbe calkowita.");
        }
    }
}

char inputChars(string message, string validChars)
{
    Console.WriteLine(message);
    while (true)
    {
        string? input = Console.ReadLine();
        if (input != null && input.Length == 1 && validChars.Contains(input[0]))
        {
            return input[0];
        }
        else
        {
            Console.WriteLine($"Bledne dane. Mozesz podac jedynie: {validChars}.");
        }
    }
}

int add(int a, int b)
{
    return a + b;
}

int subtract(int a, int b)
{
    return a - b;
}

int multiply(int a, int b)
{
    return a * b;
}

int divide(int a, int b)
{
    if (a == 0)
    {
        Console.WriteLine("Error: Nie można dzielić przez zero.");
        return 0;
    }
    else
    {
        return a / b;
    }
}

Console.WriteLine("Kalkulator");

int num1, num2, result = 0;
char operation, choice = 't';

do
{
    num1 = inputNumber("Podaj pierwsza liczbe:");
    num2 = inputNumber("Podaj druga liczbe:");

    operation = inputChars("Podaj operacje, ktora chcesz wykonac (+, -, *, /):", "+-*/");

    switch (operation)
    {
        case '+':
            result = add(num1, num2);
            break;
        case '-':
            result = subtract(num1, num2);
            break;
        case '*':
            result = multiply(num1, num2);
            break;
        case '/':
            result = divide(num1, num2);
            break;
    }
    Console.WriteLine("The result is: " + result);
    choice = inputChars("Czy chcesz ponownie wykonac dzialanie? (t/n)", "tn");

} while (choice == 't');
```