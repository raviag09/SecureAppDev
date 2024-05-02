# SecureAppDev

We are demonstrating the input validation, authentication, encryption, secure communication, and error handling in software development.

1. **Input Validation:** It prompts the user for input and checks if the input is valid by calling the IsValidInput method.
2. **Authentication and Authorization:** It simulates authentication and authorization by checking if the user input is an admin username.
3. **Data Encryption:** It encrypts sensitive data using symmetric cryptography with the AES algorithm.
4. **Secure Communication:** It communicates with a remote server over HTTPS using the HttpClient class to demonstrate secure communication.
5. **Error Handling:** It demonstrates error handling by catching exceptions that might occur during execution and providing appropriate error messages.



# Console Application Demonstrating Secure Software Development Concepts
```


using System;
using System.Net.Http;
using System.Security.Cryptography;

class Program
{
    static void Main(string[] args)
    {
        // Input Validation
        Console.WriteLine("Input Validation:");
        string userInput = Console.ReadLine();

        if (IsValidInput(userInput))
        {
            Console.WriteLine("Valid username provided");
        } else
        {
            Console.WriteLine("Invalid input detected");
            return;
        }

        // Authentication and Authorization
        Console.WriteLine("Press enter to continue");
        Console.ReadLine();
        Console.WriteLine("Authentication and Authorization:");
        if (IsAdmin(userInput))
        {
            Console.WriteLine("Access provided. User has admin rights.");
        } else
        {
            Console.WriteLine("Access denied. Admin rights required.");
            return;
        }

        // Data Encryption
        Console.WriteLine("Press enter to continue");
        Console.ReadLine();
        Console.WriteLine("Data Encryption:");
        string dataToEncrypt = "SensitiveData123";
        string encryptionKey = "U2FsdGVkX18l0fQ43M2onJ32wWQdEEXx";
        string encryptedData = Encrypt(dataToEncrypt, encryptionKey);
        Console.WriteLine("Encrypted data: " + encryptedData);

        // Secure Communication
        Console.WriteLine("Press enter to continue");
        Console.ReadLine();
        Console.WriteLine("Secure Communication:");
        using (var client = new HttpClient())
        {
            client.BaseAddress = new Uri("https://jsonplaceholder.typicode.com");

            HttpResponseMessage response = client.GetAsync("posts").Result;
            if (response.IsSuccessStatusCode)
            {
                Console.WriteLine("Secure communication successful");
            }
            else
            {
                Console.WriteLine("Failed to communicate securely");
            }
        }

        // Error Handling
        Console.WriteLine("Press enter to continue");
        Console.ReadLine();
        Console.WriteLine("Error Handling:");
        try
        {
            // Code that might throw exceptions
            int result = Divide(10, 0); // This will throw a DivideByZeroException
            Console.WriteLine("Result: " + result); // This line won't be executed if an exception occurs
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
	        Console.WriteLine("Press enter to end");
            return;
        }
    }

    static bool IsValidInput(string input)
    {
        // Perform input validation logic
        return !string.IsNullOrEmpty(input);
    }

    static bool IsAdmin(string user)
    {
        // Perform authentication and authorization logic
        if (user == "admin")
            return true; // Simulated admin access for demonstration
        else
            return false;
    }

    static string Encrypt(string data, string key)
    {
        // Perform data encryption using symmetric cryptography
        using (Aes aesAlg = Aes.Create())
        {
            aesAlg.Key = Convert.FromBase64String(key);
            aesAlg.IV = new byte[aesAlg.BlockSize / 8]; // Initialization vector

            ICryptoTransform encryptor = aesAlg.CreateEncryptor(aesAlg.Key, aesAlg.IV);
            byte[] encryptedBytes = encryptor.TransformFinalBlock(
                System.Text.Encoding.UTF8.GetBytes(data), 0, data.Length);

            return Convert.ToBase64String(encryptedBytes);
        }
    }

    public static int Divide(int dividend, int divisor)
    {
        // Check if the divisor is zero
        if (divisor == 0)
        {
            // Throw a DivideByZeroException
            throw new DivideByZeroException("Cannot divide by zero.");
        }

        // Perform the division and return the result
        return dividend / divisor;
    }
}





```
