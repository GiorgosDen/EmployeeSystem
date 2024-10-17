# EmployeeSystem
It is a simple system for managing employees, depending on the user's role. The system has three user roles: the simple User, the Assistant, and the Director, and a user can have one or multiple roles. Also, the roles have a hierarchy:

**1st: Director:** He can Delete, Update, Add, and Read all employees

**2nd: Assistant:** He can do anything like the Director, except Delete employees

**3rd: User:** He can only Read all Employees

When a user logs in to the system, he gets an Access Token with a 2-minute lifetime. In this 2-minute range, he can use his rights based on hierarchy, but if he doesn't log out or refresh the page, he continues seeing the employees' information.

## Implementation Description
This system has 3 parts: The front (user page), the back (APIs), and the database (user and employee data). In this phase, all parts had developed to execute locally, specifically:

**The front:** This React project uses Vite and Typescript. It offers a simple and completely functional UI and sends requests using axios. Based on the responses, the front allows users to connect, and manage the employees by providing users sufficient feedback for each action. Normally, the front needs more work to solve some issues (like the alert messages and some design details), but in this case, we focus on backend development (i.e. the API), and the front provides a more realistic (for ThunderClient) environment for testing the API. Front repository, https://github.com/GiorgosDen/EmployeeSystemFrontend.

**The back:** This is a NodeJS project that contains the APIs to communicate with the Database. It is responsible for following the regulations in the user's communication with the database, and providing the appropriate authorization. To test the API, I used the ThunderClient in Visual Studio. Back repository, https://github.com/GiorgosDen/EmployeeSystemBackend.

**The database:** The MySQL workbench was used. The database has 4 tables: User, Employee, UserRole, and UserConnRol.



## Photos
### Data Base Structure 
![](./EmployeeSystemPhotos/employeeSystemDB.png)
### Test Back in VS Code
I have many things to show from testing the back, but I will be trying to provide screenshots of the most important functions:

### For address localhost:3500/:
1. Success Login (POST request)
   ![](./EmployeeSystemPhotos/testLoginAPI.png)
   ! Explanation: When the username and password represent a user, the response has the access token, the username, and the role codes.
   
### For address localhost:3500/homePage:
1. Success Get Request (returns the employees)
   ![](./EmployeeSystemPhotos/successGET.png)
   ! Explanation: By using a valid access token, returned the data of employees.
   
2. Conflict Error (refers to PUT & POST Requests)
   ![](./EmployeeSystemPhotos/conflictAFM.png)
   ! Explanation: I'm trying to change the employee AFM to a bound (from another employee) AFM.
   
3. Unauthorized Error (refers to POST,  PUT,  DELETE Requests)
   ![](./EmployeeSystemPhotos/unautorizedADD.png)
   ! Explanation: I'm trying to add a new employee as a User, which doesn't have the authority to do that. If I had the code 3045 or 5021 (Assistant or Director code), then I would add the new employee.
   
4. Forbidden Error (refers to all Requests)
   ![](./EmployeeSystemPhotos/expToken.png)
   ! Explanation: I've connected for more than 2 minutes and my Access Token has expired.
   
### See Front in Browser 
Same with the back, I have many things to show, but I will be trying to provide screenshots of the most important functions/pages:
1. Login Form
   ![](./EmployeeSystemPhotos/login.png)
   ! Explanation: I'm trying to log in without a password, so the page prints a warning. Also, the page prints warnings fields in general and about the inability to locate the user, in a similar way.
   
2. Main Page
   ![](./EmployeeSystemPhotos/mainPage.png)
   ! Explanation: This is the page to manage the employees. The Main Page has a countdown clock that shows the Access Token's remaining lifetime, a list with employees' names to choose a specific employee, and the employee's card with the information. In the screenshot, the employee Georgios Denesidis has been selected.
    
3. Add Employee Form (The Update Form has the same design)
   ![](./EmployeeSystemPhotos/addForm.png)
   ! Explanation: This form appears when a user clicks the Add button, and contains all necessary fields to create a new employee. Every field label has an icon (!) on the right that prints the limitations of the current field while the mouse touches it. In this screenshot, the error follows the user trying, to add an employee without changing the fields' first values.
   
4. Delete Error
   ![](./EmployeeSystemPhotos/deleteError.png)
   ! Explanation: This error appears when a user clicks the Delete button without selecting an employee.
   
5. Unauthorized Error
   ![](./EmployeeSystemPhotos/authorizederror.png)
   ! Explanation: When a user tries to perform a function without the authority, the system prints a warning like: <Function> Error: You are not authorized to <Fuction> Employees. In this case, an unauthorized user tries to delete an employee, so the system prints the error: Delete Error: You are not authorized to delete Employees.
   
6. Token Expired Error
   ![](./EmployeeSystemPhotos/tokenExpired.png)
   ! Explanation: When the countdown timer or in other words, the 2 minutes have passed, the Access Token expires, and the user can't perform any function. He can only see the employees until trying some function. So the system prints an error like in case that screenshot.
   
