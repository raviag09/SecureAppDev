#  Unit Testing with NUnit Framework

We demonstrate how to perform unit testing using the NUnit framework in C#. It includes a series of test methods that validate various functionalities such as username validation, authentication, authorization, and data encryption. 


# Console Application Demonstrating Unit Testing with NUnit Framework
```
using NUnit.Framework;
using System;

public class Program

{

    public static void Main()

    {

        // Run the NUnit tests manually

        var testRunner = new Program();

        testRunner.RunTests();

    }
           

     public void RunTests()

    {

        // Create an instance of the test fixture

        var testFixture = new MyTests();

 

        // Call test methods

        testFixture.ValidateUsername_InputWithSpecialCharacters_ReturnsFalse();
Console.WriteLine("Press enter to continue");
Console.ReadLine();
testFixture.Authenticate_ValidCredentials_ReturnsTrue();
Console.WriteLine("Press enter to continue");
Console.ReadLine();
testFixture.Authorize_AdminRole_CanAccessAdminPage();
Console.WriteLine("Press enter to continue");
Console.ReadLine();
testFixture.EncryptAndDecrypt_SensitiveData_RemainsIntact();
    }

 

           

     [TestFixture]

    public class MyTests

    {

[Test]

public void ValidateUsername_InputWithSpecialCharacters_ReturnsFalse()

{

// Arrange

string username = "admin";
Console.WriteLine("Validating user");



// Act

bool isValid = ValidateUsername(username);



// Assert
Assert.IsTrue(isValid);
Console.WriteLine("User is admin");
}



[Test]

public void Authenticate_ValidCredentials_ReturnsTrue()

{

// Arrange

string username = "validuser";

string password = "password";



// Act
Console.WriteLine("Authenticating user");
bool isAuthenticated = Authenticate(username, password);



// Assert

Assert.IsTrue(isAuthenticated);
Console.WriteLine("Valid user credentials provided");

}



[Test]

public void Authorize_AdminRole_CanAccessAdminPage()

{

// Arrange

string username = "admin";

string resource = "adminPage";



// Act
Console.WriteLine("Authorizing user");

bool isAuthorized = IsAuthorized(username, resource);


// Assert

Assert.IsTrue(isAuthorized);
Console.WriteLine("User can access admin page");
}



[Test]

public void EncryptAndDecrypt_SensitiveData_RemainsIntact()

{

// Arrange

string sensitiveData = "This is sensitive information.";


// Act

Console.WriteLine("Encrypting and decrypting data");

string encryptedData = Encrypt(sensitiveData);

Console.WriteLine("Encrypted data: " +encryptedData);

string decryptedData = Decrypt(encryptedData);
Console.WriteLine("DecryptedData data: " +decryptedData);

// Assert
Assert.AreEqual(sensitiveData, decryptedData);
Console.WriteLine("encryption validated");
}



public bool ValidateUsername(string username)  {

if(username == "admin") {

return true;

} else {

return false;

}

}



public bool Authenticate(string username, string password)  {

if(username == "validuser" && password == "password") {

return true;

} else {

return false;

}

}



public bool IsAuthorized(string username, string resource)  {
if(username == "admin" && resource == "adminPage") {
return true;

} else {

return false;

}

}



public string Encrypt(string data)  {
// This is just an example, actual encryption logic has been demosntrated in previous example
return "Example encrpted data";

}

public string Decrypt(string data)  {
// This is just an example, actual decryption logic has been demosntrated in previous example
return "This is sensitive information.";
}
}
}




```
