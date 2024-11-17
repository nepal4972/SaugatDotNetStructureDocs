# Step-by-Step Guide to Create a Multi-Project Solution in Visual Studio

## Step 1: Open Visual Studio
- Launch Visual Studio.
- If you don’t have Visual Studio installed, download and install it from the official [Visual Studio website](https://visualstudio.microsoft.com/). The free **Community Edition** is sufficient.

## Step 2: Create a New Solution
1. From the **Start Page** or the **File** menu, select **Create a new project**.
2. In the project template list, search for and select **Blank Solution** (if not listed).
3. Click **Next**.
4. Name your solution (e.g., **MySolution**).
5. Choose the location to save the solution.
6. Click **Create**.

## Step 3: Add Projects to the Solution
Once the solution is created, you will add multiple projects: **Project.Core**, **Project.Data**, **Project.Api**, and **Project.Business**.

### Add the `Project.Core` Class Library:
1. Right-click on the **Solution** in the **Solution Explorer**.
2. Select **Add → New Project**.
3. From the list of project templates, select **Class Library (.NET Core)** (or **Class Library (.NET Standard)** depending on your version).
4. Name the project **Project.Core**.
5. Click **Create**.

### Add the `Project.Data` Class Library:
1. Right-click on the **Solution** again.
2. Select **Add → New Project**.
3. Choose **Class Library (.NET Core)** (or **Class Library (.NET Standard)**).
4. Name the project **Project.Data**.
5. Click **Create**.

### Add the `Project.Api` ASP.NET Core Web API:
1. Right-click on the **Solution** again.
2. Select **Add → New Project**.
3. From the list of project templates, choose **ASP.NET Core Web API**.
4. Name the project **Project.Api**.
5. Click **Create**.
6. Choose **API** as the template (make sure to select **.NET 6** or the version you are using).

### Add the `Project.Business` Class Library:
1. Right-click on the **Solution** once more.
2. Select **Add → New Project**.
3. Choose **Class Library (.NET Core)** (or **Class Library (.NET Standard)**).
4. Name the project **Project.Business**.
5. Click **Create**.

## Step 4: Add References Between Projects
Now that all the projects are created, you need to add references between them to enable communication.

## Small Reference

## Project References

### Project.Api
**References:**
- **Project.Core**: To access interfaces and models.
- **Project.Business**: To access business services.

### Project.Business
**References:**
- **Project.Core**: To access interfaces and models.
- **Project.Data**: To access repositories for data manipulation.

### Project.Data
**References:**
- **Project.Core**: To access models and interfaces like repositories.

### Project.Core
**References:**
- **None**: This is the foundational project and does not reference any other projects. It contains only interfaces and models that will be used across the other projects.

---

## Summary of References

- **Project.Api** references both **Project.Core** and **Project.Business**.
- **Project.Business** references **Project.Core** and **Project.Data**.
- **Project.Data** references **Project.Core**.
- **Project.Core** does not reference anything else.

---

This structure ensures that each project has access to the necessary dependencies while maintaining a clean separation of concerns.

## Big Reference

### Add `Project.Core` Reference to `Project.Data` and `Project.Api`:
1. In **Solution Explorer**, right-click on the **Dependencies** folder of **Project.Data**.
2. Select **Add → Reference**.
3. In the dialog that opens, check the box next to **Project.Core** to add it as a reference.
4. Click **OK**.
5. Repeat these steps for **Project.Api** to add **Project.Core** as a reference.

### Add `Project.Data` Reference to `Project.Api`:
1. In **Solution Explorer**, right-click on the **Dependencies** folder of **Project.Api**.
2. Select **Add → Reference**.
3. In the dialog, check the box next to **Project.Data**.
4. Click **OK**.

### Add `Project.Business` Reference to `Project.Api` and `Project.Data`:
1. In **Solution Explorer**, right-click on the **Dependencies** folder of **Project.Api**.
2. Select **Add → Reference**.
3. In the dialog, check the box next to **Project.Business**.
4. Click **OK**.
5. Repeat the steps for **Project.Data** if required.

## Step 5: Implement Basic Functionality in Each Project

### `Project.Core`:
This layer contains interfaces and models used across the application.

- Add **Interfaces** for services (e.g., `IUserService`).
- Add **Models** that represent the data structure (e.g., `User`, `Product`).
- Implement shared business logic or validation methods here.

Example: `IUserService.cs` interface

```csharp
namespace Project.Core.Interfaces
{
    public interface IUserService
    {
        User GetUserById(int id);
        IEnumerable<User> GetAllUsers();
    }
}


api -> buisnedd
buisness -> core and data
data -> core
