# SecureAppDev

Let's simulate a simple C# application that processes user authentication and authorization, and then we'll identify potential STRIDE threats within the code.

1. Spoofing: Impersonation of legitimate users due to weak authentication, enabling unauthorized access.

2. Tampering: Unauthorized alteration of application data or behavior, bypassing security controls.

3. Repudiation: Users deny actions due to lack of logging, hindering accountability and tracking of activities.

4. Information Disclosure: Vulnerabilities lead to unauthorized access or exposure of sensitive data.

5. Denial of Service (DoS): Disruption of service availability through overwhelming requests or system crashes.

6. Elevation of Privilege: Exploiting weak authentication to gain unauthorized access to sensitive areas or escalate privileges.

# Console Application Demonstrating Secure Software Development Concepts

```

using System;

class Program
{
    static void Main(string[] args)
    {
        // Simulating an application with authentication and authorization
        Console.WriteLine("Enter username:");
        string username = Console.ReadLine();
        Console.WriteLine("Enter password:");
        string password = Console.ReadLine();

        if (AuthenticateUser(username, password))
        {
            Console.WriteLine("User authenticated successfully.");
            Console.WriteLine("Accessing sensitive data...");
            AccessSensitiveData();
        }
        else
        {
            Console.WriteLine("Authentication failed. Access denied.");
        }
    }

    static bool AuthenticateUser(string username, string password)
    {
        // Simulated authentication logic
        if (username == "admin" && password == "password123")
        {
            // Authorized user
            return true;
        }
        else
        {
            // Unauthorized user
            return false;
        }
    }

    static void AccessSensitiveData()
    {
        // Simulated access to sensitive data
        Console.WriteLine("Accessing sensitive data...");
        Console.WriteLine("Sensitive data accessed successfully.");
    }
}




```
