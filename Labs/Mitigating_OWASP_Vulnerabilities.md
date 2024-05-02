# Mitigating OWASP Vulnerabilities in C# Code

Demonstrating the simulation strategies to help safeguard against the top OWASP vulnerabilities. 
 
 top scanning tools commonly used to mitigate OWASP vulnerabilities:

1. Nessus - widely-used vulnerability scanner that helps identify security issues, misconfigurations, and compliance violations
2. Burp Suite: Burp Suite is a popular toolkit for web application security testing. automatically detect OWASP Top 10 vulnerabilities like SQL injection, XSS, and CSRF
3. Acunetix: Acunetix is a web vulnerability scanner designed to identify security vulnerabilities in web applications, including those outlined in the OWASP Top 10
4. OWASP ZAP (Zed Attack Proxy): OWASP ZAP is an open-source web application security scanner maintained by the OWASP community. automated scanning, active and passive security testing, and integration with CI/CD pipelines.


### Mitigating OWASP Vulnerabilities in C# Code



## 1.SQL Injection:
```
using System;
using System.Data.SqlClient;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Enter username: ");
        string username = Console.ReadLine();
        
        // Vulnerable SQL query with string concatenation
        string query = "SELECT * FROM Users WHERE Username = '" + username + "'";
        
        // Execute query (for demonstration purposes only; do not use in production)
        using (SqlConnection connection = new SqlConnection("your_connection_string"))
        {
            SqlCommand command = new SqlCommand(query, connection);
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();
            
            // Process query result
            while (reader.Read())
            {
                Console.WriteLine("User found: " + reader["Username"]);
            }
        }
    }

```

you can fix the SQL vulnerabilities in multiple ways. Below are 2 approaches. 

```
//parameterized queries
string query = "SELECT * FROM Users WHERE Username = @Username";
using (SqlConnection connection = new SqlConnection(connectionString))
{
    SqlCommand command = new SqlCommand(query, connection);
    command.Parameters.AddWithValue("@Username", username);
    connection.Open();
    SqlDataReader reader = command.ExecuteReader();
    // Process query result
}

```

```
// Stored procedures
using (SqlConnection connection = new SqlConnection(connectionString))
{
    SqlCommand command = new SqlCommand("sp_GetUserByUsername", connection);
    command.CommandType = CommandType.StoredProcedure;
    command.Parameters.AddWithValue("@Username", username);
    connection.Open();
    SqlDataReader reader = command.ExecuteReader();
    // Process query result
}
```




## 2.	Cross-Site Scripting (XSS):If an attacker enters malicious input containing HTML or JavaScript code, it will be included in the output string as-is.  

```
using System;
using System.Web;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Enter your name: ");
        string name = Console.ReadLine();
        
        // Vulnerable code with unencoded output
        string output = "<h1>Welcome, " + name + "!</h1>";
        
        // Render output (for demonstration purposes only; do not use in production)
        Console.WriteLine("Rendered output: " + output);
    }
}

```

Here's how you can fix the code by encoding the output:

```

using System;
using System.Web;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Enter your name: ");
        string name = Console.ReadLine();
        
        // Encode user input to prevent XSS attacks
        string encodedName = HttpUtility.HtmlEncode(name);
        
        // Safe output with encoded user input
        string output = "<h1>Welcome, " + encodedName + "!</h1>";
        
        // Render output
        Console.WriteLine("Rendered output: " + output);
    }
}

```

## 3.	Insecure Direct Object References (IDOR): An attacker could potentially manipulate the index input to access files that they are not authorized to view. 

```

using System;

public class Program
{
    private static string[] secretFiles = { "file1.txt", "file2.txt", "file3.txt" };

    public static void Main()
    {
        Console.WriteLine("Enter file index (0-2): ");
        int index = Convert.ToInt32(Console.ReadLine());

        // Access file without proper authorization check
        string file = secretFiles[index];

        // Display file content (for demonstration purposes only; do not use in production)
        Console.WriteLine("File content: " + file);
    }
}


```


To mitigate IDOR vulnerabilities, proper authorization checks should be implemented to ensure that users can only access files that they are authorized to view. 

```
using System;

public class Program
{
    private static string[] secretFiles = { "file1.txt", "file2.txt", "file3.txt" };

    public static void Main()
    {
        Console.WriteLine("Enter file index (0-2): ");
        int index;
        if (!int.TryParse(Console.ReadLine(), out index) || index < 0 || index >= secretFiles.Length)
        {
            Console.WriteLine("Invalid file index.");
            return;
        }

        // Simulate user role (for demonstration purposes)
        string userRole = GetUserRole();

        // Perform authorization check before accessing file
        if (IsAuthorizedToAccessFile(index, userRole))
        {
            string file = secretFiles[index];
            Console.WriteLine("File content: " + file);
        }
        else
        {
            Console.WriteLine("You are not authorized to access this file.");
        }
    }

    private static string GetUserRole()
    {
        // Simulate user role retrieval (for demonstration purposes)
        // Replace with actual logic to retrieve user role from authentication system
        // For simplicity, we'll assume all users have the same role
        return "user1";
    }

    private static bool IsAuthorizedToAccessFile(int index, string userRole)
    {
        // Define roles and associated permissions
        // For demonstration purposes, we'll allow 'admin' role to access all files
        // 'user' role is only allowed to access files 0 and 1
        if (userRole == "admin")
        {
            return true; // Admin has access to all files
        }
        else if (userRole == "user")
        {
            return index >= 0 && index <= 1; // User can only access files 0 and 1
        }
        else
        {
            return false; // Other roles have no access by default
        }
    }
}

```

## 4.	Sensitive Data Exposure:

```
using System;

public class Program
{
    public static void Main()
    {
        string apiKey = "your_sensitive_api_key";
        
        // Vulnerable code exposing sensitive API key
        Console.WriteLine("API key: " + apiKey);
    }
}
```


To mitigate this vulnerability, sensitive information like API keys should be handled securely
   •	Storing API keys in secure configuration files 
   •	Accessing API keys through secure methods
 






