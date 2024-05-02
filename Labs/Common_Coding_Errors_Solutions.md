# Common Coding Errors and Secure Solutions

This collection covers various security vulnerabilities frequently encountered in software development

1. Buffer Overflows: Writing too much data to a fixed-size buffer, risking memory corruption.
2. Format String Problems: Using user input directly in format strings, leading to vulnerabilities.
3. Integer Overflows: Arithmetic operations causing values outside data type's range.
4. SQL Injection: Concatenating user input into SQL queries, enabling injection attacks.
5. Command Injection: Executing shell commands with unsanitized user input, risking arbitrary command execution.
6. Cross-site Scripting (XSS): Including untrusted data in web pages without proper encoding, enabling script execution.
7. Failing to Protect Network Traffic: Downloading data over unencrypted connections, risking interception.
8. Improper Use of SSL/TLS: Using outdated or insecure versions of SSL/TLS protocols.
9. Use of Weak Password-Based Systems: Employing easily guessable or crackable passwords.
10. Failing to Store & Protect Data Securely: Storing sensitive data without encryption, risking exposure.
11. Trusting Network Name Resolution: Relying on insecure methods for DNS resolution, risking attacks.
12. Race Conditions: Inconsistent results due to multiple threads accessing shared data unsynchronized.


# Demonstrating the Common Security Vulnerabilities in Software Development and remediations.Each fixed code snippet addresses the vulnerabilities present in the original code, 
making the applications more secure against potential threats.


## 1. Buffer Overflows:
```
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with potential buffer overflow
        string[] buffer = new string[2];
        buffer[0] = "First";
        buffer[1] = "Second";
        buffer[2] = "Third"; // Potential buffer overflow if more elements are added
        
        // Fixed code with dynamic array resizing
        List<string> dynamicBuffer = new List<string>();
        dynamicBuffer.Add("First");
        dynamicBuffer.Add("Second");
        dynamicBuffer.Add("Third"); 
		dynamicBuffer.Add("fourth");// No buffer overflow risk
    }
}


```


## 2. Format String Problems 

```
using System;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with format string vulnerability
        string userInput = "User Input";
        Console.WriteLine(userInput); // Potential format string vulnerability
        
        // Fixed code with string concatenation or formatting
        Console.WriteLine("User Input: " + userInput); // Safe from format string vulnerability
    }
}


```



## 3. Integer Overflows:

```
using System;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with potential integer overflow
        int maxValue = int.MaxValue;
        int incrementedValue = maxValue + 1; // Potential integer overflow
        
        // Fixed code with range checking
        if (maxValue < int.MaxValue)
        {
            incrementedValue = maxValue + 1; // Prevents integer overflow
        }
        else
        {
            Console.WriteLine("Integer overflow detected!");
        }
    }
}


```



## 4. SQL Injection:

```
using System;
using System.Data.SqlClient;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with SQL injection vulnerability
        string userInput = "'; DROP TABLE Users; --";
        string query = "SELECT * FROM Users WHERE Username = '" + userInput + "'";
        // Fixed code with parameterized queries
        string query = "SELECT * FROM Users WHERE Username = @Username";
        SqlCommand command = new SqlCommand(query, connection);
        command.Parameters.AddWithValue("@Username", userInput);
    }
}


```



## 5. Command Injection:

```
using System;
using System.Diagnostics;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with command injection vulnerability
        string userInput = "file.txt; rm -rf /";
        Process.Start("cmd.exe", "/c copy " + userInput + " c:\\temp");
        
        // Fixed code with safe command execution
        Process.Start("cmd.exe", "/c copy file.txt c:\\temp"); // Hardcoded command path
    }
}



```



## 6. Failing to Handle Errors:

```

using System;

public class Program
{
    public static void Main()
    {
        try
        {
            // Vulnerable code without error handling
            int[] numbers = { 1, 2, 3 };
            Console.WriteLine(numbers[5]); // Potential index out of range exception
        }
        catch (Exception ex)
        {
            // Fixed code with error handling
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }
}

```



## 7. Cross-site Scripting (XSS):

```
using System;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with potential XSS vulnerability
        string userInput = "<script>alert('XSS attack');</script>";
        Console.WriteLine(userInput); // Potential XSS vulnerability
        
        // Fixed code with HTML encoding
        Console.WriteLine(System.Web.HttpUtility.HtmlEncode(userInput)); // Safe from XSS
    }
}


```



## 8. Failing to Protect Network Traffic:

```

using System;
using System.Net;

public class Program
{
    public static void Main()
    {
        // Vulnerable code without encryption
        WebClient client = new WebClient();
        string response = client.DownloadString("http://example.com"); // Potential network traffic interception
        
        // Fixed code with HTTPS
        ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;
        string response = client.DownloadString("https://example.com"); // Secure network traffic
    }
}



```



## 9. Improper Use of SSL and TLS:

```
using System;
using System.Net;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with outdated SSL/TLS version
        ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls;
        WebClient client = new WebClient();
        string response = client.DownloadString("https://example.com"); // Vulnerable to SSL/TLS vulnerabilities
        
        // Fixed code with updated SSL/TLS version
        ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;
        string response = client.DownloadString("https://example.com"); // Secure SSL/TLS connection
    }
}


```



## 10. Use of Weak Password-Based Systems:

```
using System;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with weak password
        string password = "123456";
        // Fixed code with strong password policy
        string password = "P@ssw0rd!"; // Strong password with complexity requirements
    }
}


```



## 11. Failing to Store & Protect Data Securely:

```
using System;
using System.IO;
using System.Security.Cryptography;

public class Program
{
    public static void Main()
    {
        // Vulnerable code storing sensitive data without encryption
        string password = "sensitive_password";
        Console.WriteLine("Password stored: " + password); // Potential data exposure
        
        // Fixed code with secure data storage using encryption
        byte[] dataToEncrypt = System.Text.Encoding.UTF8.GetBytes("sensitive_password");
        using (Aes aes = Aes.Create())
        {
            aes.Key = new byte[32]; // Replace with a securely generated key
            aes.IV = new byte[16]; // Replace with a securely generated IV
            byte[] encryptedData = Encrypt(dataToEncrypt, aes.Key, aes.IV);
            Console.WriteLine("Encrypted password stored: " + Convert.ToBase64String(encryptedData));
        }
    }
    
    // Encryption function
    static byte[] Encrypt(byte[] data, byte[] key, byte[] iv)
    {
        using (Aes aesAlg = Aes.Create())
        {
            aesAlg.Key = key;
            aesAlg.IV = iv;
            ICryptoTransform encryptor = aesAlg.CreateEncryptor(aesAlg.Key, aesAlg.IV);
            using (MemoryStream msEncrypt = new MemoryStream())
            {
                using (CryptoStream csEncrypt = new CryptoStream(msEncrypt, encryptor, CryptoStreamMode.Write))
                {
                    csEncrypt.Write(data, 0, data.Length);
                    csEncrypt.FlushFinalBlock();
                    return msEncrypt.ToArray();
                }
            }
        }
    }
}

```



## 12. Trusting Network Name Resolution: 

```
// This code might throw an error Request for the permission of type 'System.Net.DnsPermission. 

using System;
using System.Net;

public class Program
{
    public static void Main()
    {
        // Vulnerable code trusting network name resolution
        IPAddress[] addresses = Dns.GetHostAddresses("example.com");
        foreach (IPAddress address in addresses)
        {
            Console.WriteLine("IP Address: " + address.ToString()); // Potential DNS spoofing or cache poisoning
        }
        
        // Fixed code with explicit IP address validation
        IPAddress ipAddress;
        if (IPAddress.TryParse("example.com", out ipAddress))
        {
            Console.WriteLine("IP Address: " + ipAddress.ToString());
        }
        else
        {
            Console.WriteLine("Invalid host name");
        }
    }
}

// This code will fix it

using System;
using System.Net;

public class Program
{
    public static void Main()
    {
        // Fixed code with explicit IP address validation
        IPAddress ipAddress;
        if (IPAddress.TryParse("example.com", out ipAddress))
        {
            Console.WriteLine("IP Address: " + ipAddress.ToString());
        }
        else
        {
            Console.WriteLine("Invalid host name");
        }
}
}



```





## 13. Race conditions

```

using System;
using System.Threading;

public class Program
{
    private static int balance = 100;

    public static void Main()
    {
        Thread thread1 = new Thread(WithdrawMoney);
        Thread thread2 = new Thread(WithdrawMoney);

        thread1.Start(100);
        thread2.Start(200);
    }

    private static void WithdrawMoney(object amount)
    {
        int withdrawalAmount = (int)amount;
        if (balance >= withdrawalAmount)
        {
            Thread.Sleep(100); // Simulate processing time
            balance -= withdrawalAmount;
            Console.WriteLine("Withdrawal successful. Remaining balance: " + balance);
        }
        else
        {
            Console.WriteLine("Insufficient funds.");
        }
    }
}



```



## 14. Unauthenticated Key Exchange:

```
using System;
using System.Security.Cryptography;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with unauthenticated key exchange
        using (ECDiffieHellmanCng client = new ECDiffieHellmanCng())
        {
            byte[] clientPublicKey = client.PublicKey.ToByteArray(); // Potential interception of public key
            // Send clientPublicKey to server
        }

        // Fixed code with authenticated key exchange
        using (ECDiffieHellmanCng client = new ECDiffieHellmanCng())
        {
            CngKey clientPrivateKey = client.Key;
            byte[] clientPublicKey = client.PublicKey.ToByteArray();
            // Send clientPublicKey to server along with a digital signature
            // Server verifies the digital signature before using the public key
        }
    }
}


```


## 15. Not using Cryptographically Strong Random Numbers:

```


using System;
using System.Security.Cryptography;

public class Program
{
    public static void Main()
    {
        // Vulnerable code using insecure random number generator
        Random insecureRandom = new Random(); // Insecure random number generator
        int insecureRandomNumber = insecureRandom.Next(); // Insecure random number
        
        // Fixed code using cryptographically secure random number generator
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            byte[] randomBytes = new byte[4]; // Adjust the byte length as needed
            rng.GetBytes(randomBytes);
            int randomNumber = BitConverter.ToInt32(randomBytes, 0);
            Console.WriteLine("Cryptographically secure random number: " + randomNumber);
        }
    }
}

```


##  16. Poor Usability:

```
using System;

public class Program
{
    public static void Main()
    {
        // Vulnerable code with poor usability
        Console.WriteLine("Please enter your password: "); // No guidance or feedback
        
        // Fixed code with improved usability
        Console.WriteLine("Please enter your password (at least 8 characters long): "); // Clear guidance to the user
    }
}


```



