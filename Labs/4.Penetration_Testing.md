# Penetration Testing

Penetration testing, commonly referred to as "pen testing," is a proactive security assessment technique used to identify vulnerabilities in an organization's IT infrastructure,
applications, and networks.
 
 
Industry scanning tools for penetration testing include:

1. Nmap (Network Mapper): A powerful open-source network scanning tool used to discover hosts and services on a computer network.
2. Metasploit: An advanced open-source penetration testing framework that helps security professionals assess vulnerabilities and manage security assessments.
3. Burp Suite: A comprehensive set of tools for web application security testing, including scanning, crawling, and exploitation.
4. Wireshark: A widely-used network protocol analyzer that allows security professionals to capture and analyze network traffic in real-time.
5. Nessus: A vulnerability scanning tool that identifies security vulnerabilities, configuration issues, and malware in networks, systems, and applications.
6. OpenVAS (Open Vulnerability Assessment System): An open-source vulnerability scanner that performs comprehensive vulnerability assessments and provides a centralized management interface.
7. Acunetix: A web vulnerability scanner that automatically detects and reports web application vulnerabilities, including SQL injection, cross-site scripting (XSS), and insecure server configurations.
8. SQLMap: A popular open-source penetration testing tool that automates the process of detecting and exploiting SQL injection vulnerabilities in web applications.



### Penetration Testing Simulation in C# - Demonstrating Network Scanning, SQL Injection, and XSS Attacks.
```

using System;

public class Program
{
    public static void Main()
    {
        Console.WriteLine("Starting penetration testing...");

        // Simulate penetration testing actions
        SimulateNetworkScan();
        SimulateSQLInjection();
        SimulateXSSAttack();

        Console.WriteLine("Penetration testing completed.");
    }

    public static void SimulateNetworkScan()
    {
        Console.WriteLine("Simulating network scan...");
        // Simulate network scan by iterating through a list of IP addresses
        string[] ipAddresses = { "192.168.0.1", "192.168.0.2", "192.168.0.3" };
        foreach (var ip in ipAddresses)
        {
            Console.WriteLine("Scanning IP address: " + ip);
            // Simulate scanning process
            Console.WriteLine("Open ports found: 80, 443");
        }
        Console.WriteLine("Network scan completed.");
    }

    public static void SimulateSQLInjection()
    {
        Console.WriteLine("Simulating SQL injection attack...");
        // Simulate SQL injection attack by attempting to retrieve data from a vulnerable database
        string userInput = "1; DROP TABLE Users;";
        Console.WriteLine("Executing SQL query: SELECT * FROM Users WHERE id = " + userInput);
        // Dummy response from database
        Console.WriteLine("Error: Table 'Users' does not exist.");
        Console.WriteLine("SQL injection attack completed.");
    }

    public static void SimulateXSSAttack()
    {
        Console.WriteLine("Simulating XSS attack...");
        // Simulate XSS attack by injecting malicious script into a web form
        string userInput = "<script>alert('XSS attack!')</script>";
        Console.WriteLine("User input: " + userInput);
        // Dummy output on web page
        Console.WriteLine("Hello, " + userInput + "! Welcome to our website.");
        Console.WriteLine("XSS attack completed.");
    }
}





```
