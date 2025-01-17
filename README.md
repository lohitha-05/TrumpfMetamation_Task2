
# TrumpfMetamation_Task2 - Alarm Automation

## Overview

This project automates the Clock app's Alarm functionality using C# and FlaUI. The automation includes the following steps:
- Opening the Clock app.
- Navigating to the Alarm section.
- Creating a new alarm with specified details.
- Enabling the alarm.
- Verifying that the alarm is saved with the expected details.
- Deleting the alarm.
- Validating the alarm has been removed successfully.

## Tools and Technologies

- **C#**: The primary programming language used for automation.
- **FlaUI**: UI Automation library for interacting with Windows applications.
- **NUnit**: A testing framework for running automated tests.
- **Visual Studio**: Integrated Development Environment (IDE) for writing and running C# code.
- **Git**: Version control for managing project files.

## Prerequisites

1. **.NET SDK 6.0 or later**: Required for building and running the project.
   - Download and install from [here](https://dotnet.microsoft.com/download/dotnet).
   
2. **Visual Studio**: Install the **.NET Desktop Development** workload for C# development.
   - Download Visual Studio from [here](https://visualstudio.microsoft.com/).

3. **FlaUI Library**: UI automation library required to interact with the Clock app.
   - Add FlaUI via NuGet by running the following commands:
     ```bash
     dotnet add package FlaUI.Core
     dotnet add package FlaUI.UIA3
     dotnet add package NUnit
     dotnet add package NUnit3TestAdapter
     dotnet add package Microsoft.NET.Test.Sdk
     ```

## Project Setup

1. **Create the Project**:
   Run the following command to create a new NUnit test project:
   ```bash
   dotnet new mstest -n TrumpfMetamation_Task2
   ```

2. **Modify the Project File**:
   Update the project file (`.csproj`) to target the Windows platform by modifying the `<TargetFramework>` element to:
   ```xml
   <PropertyGroup>
     <OutputType>Exe</OutputType>
     <TargetFramework>net6.0-windows</TargetFramework>
   </PropertyGroup>
   ```

3. **Write the Automation Code**:
   Replace the default test file with a new file, `Task2Automation.cs`. This file will contain the automation code for interacting with the Clock app's Alarm functionality.

```csharp
using FlaUI.Core;
using FlaUI.UIA3;
using NUnit.Framework;
using System;

[TestFixture]
public class AlarmAutomation
{
    [Test]
    public void AutomateAlarmHandling()
    {
        // Open the Clock app
        var app = Application.Launch("explorer.exe");
        
        // Navigate to Alarm section
        var window = app.GetMainWindow();
        var alarmButton = window.FindFirstDescendant(cf => cf.ByName("Alarm")).AsButton();
        alarmButton.Click();

        // Create New Alarm
        var addAlarmButton = window.FindFirstDescendant(cf => cf.ByName("Add alarm")).AsButton();
        addAlarmButton.Click();

        // Set alarm time and enable it
        var timePicker = window.FindFirstDescendant(cf => cf.ByName("Time")).AsComboBox();
        timePicker.Select("06:00 AM");

        var saveButton = window.FindFirstDescendant(cf => cf.ByName("Save")).AsButton();
        saveButton.Click();

        // Verify the alarm is saved
        var alarmList = window.FindFirstDescendant(cf => cf.ByName("Alarm List"));
        Assert.IsTrue(alarmList.FindAllDescendants(cf => cf.ByText("06:00 AM")).Count > 0, "Alarm was not saved correctly.");

        // Delete the alarm
        var deleteButton = window.FindFirstDescendant(cf => cf.ByName("Delete")).AsButton();
        deleteButton.Click();

        // Validate the alarm has been removed
        Assert.IsFalse(alarmList.FindAllDescendants(cf => cf.ByText("06:00 AM")).Count > 0, "Alarm was not deleted.");
    }
}
```

4. **Build and Run the Project**:
   - To build the project:
     ```bash
     dotnet build
     ```
   - To run the tests:
     ```bash
     dotnet test
     ```

## How to Run the Project

1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```

2. Navigate into the project directory:
   ```bash
   cd TrumpfMetamation_Task2
   ```

3. Restore the dependencies:
   ```bash
   dotnet restore
   ```

4. Build the project:
   ```bash
   dotnet build
   ```

5. Run the automation tests:
   ```bash
   dotnet test
   ```

## Files in the Project

1. **Project Files**
   - `Task2Automation.cs`: Contains the automation code for handling the Alarm feature.
   - `TrumpfMetamation_Task2.csproj`: Project configuration file.

2. **Dependencies (NuGet Packages)**
   - `FlaUI.Core`: Core automation library for interacting with Windows UI.
   - `FlaUI.UIA3`: UI Automation API 3 for interacting with Windows UI.
   - `NUnit`: Testing framework for writing and running automated tests.
   - `Microsoft.NET.Test.Sdk`: Required for running tests with .NET.

## Deliverables

1. **GitHub Repository**:
   Push your project to GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit for Task2"
   git remote add origin <repository-url>
   git push -u origin main
   ```

2. **README.md**:
   Include this file in your repository.

---

## Conclusion

This project demonstrates the use of **FlaUI** for automating UI tasks in Windows applications like the Clock app. By creating and interacting with alarms, this automation simulates a real-world use case of automating UI-based workflows.
```

