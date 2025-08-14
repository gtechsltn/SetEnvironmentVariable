# Add or Remove Environment Variables

There are several ways to add or remove environment variables for a Windows C# Console App, with the best method depending on the scope you need. You can manage them at the process, user, or machine level using the System.Environment class.

+ Adding an Environment Variable
+ Removing an Environment Variable

**Để thêm một biến môi trường và sử dụng nó ở bất kỳ đâu từ CMD**, bạn cần thiết lập biến môi trường ở phạm vi máy (Machine). Việc này sẽ làm cho biến đó có hiệu lực với tất cả người dùng và tất cả các tiến trình trên máy tính.

Bạn có thể làm điều này ngay trong ứng dụng C# của mình bằng cách sử dụng lớp **```System.Environment```**.

Thêm biến môi trường ở cấp độ Máy

Sử dụng phương thức **```Environment.SetEnvironmentVariable```** và chỉ định **```EnvironmentVariableTarget.Machine```** làm tham số.

```
using System;

class Program
{
    static void Main(string[] args)
    {
        // Tên biến môi trường bạn muốn thêm
        string variableName = "MY_GLOBAL_APP_PATH";
        
        // Giá trị của biến, ví dụ: đường dẫn đến ứng dụng của bạn
        string variableValue = "C:\\MyAwesomeConsoleApp\\";

        try
        {
            // Thêm biến môi trường với phạm vi Machine.
            // Chú ý: Việc này có thể yêu cầu quyền quản trị (Administrator).
            Environment.SetEnvironmentVariable(variableName, variableValue, EnvironmentVariableTarget.Machine);
            
            Console.WriteLine($"Biến môi trường '{variableName}' đã được thêm thành công.");
        }
        catch (System.Security.SecurityException)
        {
            Console.WriteLine("Lỗi: Không đủ quyền để thêm biến môi trường cấp độ Machine. " +
                              "Vui lòng chạy ứng dụng với quyền quản trị.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Đã xảy ra lỗi: {ex.Message}");
        }

        // Sau khi thêm, biến này sẽ có hiệu lực trong các cửa sổ CMD mới mở.
        Console.WriteLine("Hãy mở một cửa sổ CMD mới và gõ 'echo %MY_GLOBAL_APP_PATH%' để kiểm tra.");
    }
}
```

## Lưu ý quan trọng:

+ **Quyền quản trị**: Để thiết lập biến môi trường ở cấp độ máy, bạn cần chạy ứng dụng Console App với quyền quản trị viên (Run as administrator). Nếu không, chương trình sẽ báo lỗi SecurityException.
+ **Hiệu lực tức thì**: Biến môi trường mới sẽ không có hiệu lực ngay lập tức trong các cửa sổ CMD đang mở. Bạn cần mở một cửa sổ CMD mới để các thay đổi có hiệu lực.
+ **Đọc biến môi trường**: Để đọc giá trị của biến môi trường trong code C# của bạn, bạn sử dụng phương thức Environment.GetEnvironmentVariable và chỉ định phạm vi tương ứng.
```
string myGlobalPath = Environment.GetEnvironmentVariable("MY_GLOBAL_APP_PATH", EnvironmentVariableTarget.Machine);
Console.WriteLine($"Đường dẫn của ứng dụng: {myGlobalPath}");
```

# Adding an Environment Variable

## Scope Current Process
```
string newVariable = "MY_TEMP_VARIABLE";
string value = "Hello, World!";
Environment.SetEnvironmentVariable(newVariable, value);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable)}' to the current process.");
```

## Scope Current User
```
string newVariable = "MY_USER_VARIABLE";
string value = "User-specific data";
Environment.SetEnvironmentVariable(newVariable, value, EnvironmentVariableTarget.User);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable, EnvironmentVariableTarget.User)}' for the current user.");
```

## Scope Machine
```
string newVariable = "MY_MACHINE_VARIABLE";
string value = "Machine-wide configuration";
Environment.SetEnvironmentVariable(newVariable, value, EnvironmentVariableTarget.Machine);
Console.WriteLine($"Added '{newVariable}' with value '{Environment.GetEnvironmentVariable(newVariable, EnvironmentVariableTarget.Machine)}' for all users on the machine.");
```

# Removing an Environment Variable

## Scope Current User
```
string variableToRemove = "MY_USER_VARIABLE";
Environment.SetEnvironmentVariable(variableToRemove, null, EnvironmentVariableTarget.User);
Console.WriteLine($"Removed '{variableToRemove}' from the user scope.");
```

## Scope Current Process
```
string variableToRemove = "MY_TEMP_VARIABLE";
Environment.SetEnvironmentVariable(variableToRemove, null);
Console.WriteLine($"Removed '{variableToRemove}' from the current process.");
```
