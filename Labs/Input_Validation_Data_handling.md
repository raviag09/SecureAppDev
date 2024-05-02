# Data Handling

Here are the practices related to data handling and security in software development:

1. Canonicalization: Simplifying data to its standard form for consistency across different sources or formats.
2. Normalization: Organizing database data to minimize redundancy and improve integrity.
3. Sanitization: Removing harmful elements from data to prevent security vulnerabilities like injection attacks.
4. Blacklisting vs. Whitelisting: Control access based on predefined criteria. Blacklisting blocks specific items, while whitelisting allows only approved ones.
5. Validation: Checking data against criteria to ensure it meets standards before use, maintaining integrity and security.

# Console demonstrating Data Security Concepts


## 1. Canonicalization - Canonicalization involves converting data to its simplest 

```

using System;

public class Program
{
    public static void Main()
    {
        // Example: Canonicalizing a URL
        string originalUrl = "Http://example.com/Page?Param=Value";
        string canonicalUrl = originalUrl.ToLower(); // Convert to lowercase
        
        Console.WriteLine("Original URL: " + originalUrl);
        Console.WriteLine("Canonical URL: " + canonicalUrl);
    }
}



```
## 2. Normalization - Normalization involves transforming data into a standard format to simplify comparison and processing. 

```
using System;

public class Program
{
    public static void Main()
    {
        // Example: Normalizing an email address
        string email = "UserName@Example.COM";
        string normalizedEmail = email.ToLower(); // Convert to lowercase
        
        Console.WriteLine("Original Email: " + email);
        Console.WriteLine("Normalized Email: " + normalizedEmail);
    }
}




```

## 3. Sanitization - Sanitization involves removing or escaping potentially harmful characters 

```
using System;

public class Program
{
    public static void Main()
    {
        // Example: Sanitizing user input (removing HTML tags)
        string userInput = "<script>alert('Hello!');</script>";
        string sanitizedInput = userInput.Replace("<", "&lt;").Replace(">", "&gt;");
        
        Console.WriteLine("Original Input: " + userInput);
        Console.WriteLine("Sanitized Input: " + sanitizedInput);
    }
}



```

## 4. Blacklisting vs. Whitelisting - involves specifying what is not allowed, while whitelisting involves specifying what is allowed

```

using System;

public class Program
{
    public static void Main()
    {
        // Example: Blacklisting vs. Whitelisting
        string userInput = "<script>alert('Hello!');</script>";
        
        // Blacklisting approach (less secure)
        if (userInput.Contains("<script>"))
        {
            Console.WriteLine("Invalid input detected!");
        }
        
        // Whitelisting approach (more secure)
        if (!userInput.Contains("&lt;") && !userInput.Contains("&gt;"))
        {
            Console.WriteLine("Valid input!");
        }
    }
}

```

## 5. Validation - Validation ensures that input data meets specific criteria or rules.  


```
using System;
using System.Text.RegularExpressions;

public class Program
{
    public static void Main()
    {
        // Example: Validation (checking if an email address is valid)
        string email = "user@example.com";
        bool isValidEmail = Regex.IsMatch(email, @"^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$");
        
        if (isValidEmail)
        {
            Console.WriteLine("Valid email address!");
        }
        else
        {
            Console.WriteLine("Invalid email address!");
        }
    }
}





```








