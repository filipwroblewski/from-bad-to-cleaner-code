# from-bad-to-cleaner-code
👨‍💻🔜😊 Showing process of changeing code from bad  to cleaner one

___

## Bad code

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

## Cleaner code

```c#
/* 
------------------------------------------------------------
    Kalkulator
------------------------------------------------------------
    Prosty kalkulator obslugujacy dzialania na 2 liczbach. 
    Mozliwe dzialania do wykonania: 
        - dodawanie, 
        - odejmowanie, 
        - mnozenie, 
        - dzielenie.
    Opcja wykonywania dzialan ponownie.
------------------------------------------------------------
*/



/*Obsluga wprowadzania liczby, dopoki wartosc nie jest poprawna
przyjmuje: 
    komunikat wyswietlany podczas przypisywania liczby
zwraca: 
    liczbe calkowita*/
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

/*Obsluga wprowadzania znaku, dopoki wartosc nie jest poprawna
przyjmuje: 
    komunikat wyswietlany podczas przypisywania liczby
    ciag znakow, ktore sa akceptowane
zwraca: 
    pojedynczy znak*/
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