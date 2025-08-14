# Add or Remove Environment Variables for a Windows C# Console App

There are several ways to add or remove environment variables for a Windows C# Console App, with the best method depending on the scope you need. You can manage them at the process, user, or machine level using the System.Environment class.

+ Adding an Environment Variable
+ Removing an Environment Variable

# Adding an Environment Variable
```
string newVariable = "MY_TEMP_VARIABLE";
string value = "Hello, World!";
Environment.SetEnvironmentVariable(newVariable, value);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable)}' to the current process.");

string newVariable = "MY_USER_VARIABLE";
string value = "User-specific data";
Environment.SetEnvironmentVariable(newVariable, value, EnvironmentVariableTarget.User);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable, EnvironmentVariableTarget.User)}' for the current user.");

string newVariable = "MY_MACHINE_VARIABLE";
string value = "Machine-wide configuration";
Environment.SetEnvironmentVariable(newVariable, value, EnvironmentVariableTarget.Machine);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable, EnvironmentVariableTarget.Machine)}' for all users on the machine.");
```

# Removing an Environment Variable
```
string variableToRemove = "MY_USER_VARIABLE";
Environment.SetEnvironmentVariable(variableToRemove, null, EnvironmentVariableTarget.User);
Console.WriteLine($"Removed '{variableToRemove}' from the user scope.");

string variableToRemove = "MY_TEMP_VARIABLE";
Environment.SetEnvironmentVariable(variableToRemove, null);
Console.WriteLine($"Removed '{variableToRemove}' from the current process.");
```
