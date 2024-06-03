
### Invariants
---
Always are at the begginning of a method (except constructors). Check if objects are consistent.

### Preconditions
---
Always at the begginning of a public method. Not needed in private methods.

### PostConditions
---
Always at the end of a public method. Not needed in private methods.

````C#
public void AddUser(string userName, string plainPassword, UserData data) //no throws clause!!{ 
	
	//INVARIANT : Always at the beginning of a method (except constructors). Is object consistent? 
	Invariant(); 
	int previousUserCount = GetUserCount(); //PRECONDITIONS are not always wrong parameters: object can be in an invalid state.

	//InvalidOperationException is used 
	if (UserFileIsLocked()) 
		throw new InvalidOperationException("The file is temporally inaccessible"); 
	//If arguments have an incorrect value, ArgumentException is used. 
	if (!ValidUserName(userName)) 
		throw new ArgumentException("User name is invalid: please use a non-existing, non-null user name"); 
	if (plainPassword.Length < 10) 
		throw new ArgumentException("The password size must be at least 10"); 
	if (!PasswordWithEnoughComplexity(plainPassword)) 
		throw new ArgumentException("Password must have at least one upper and lowercase char, number and symbol"); 
	if (data == null) 
		throw new ArgumentException(("Extra user data cannot be null");
									
	//TIP: We can create our own exceptions (inheriting from the Exception class) for this, but normally //ArgumentException and InvalidOperationException are enough for most cases 
									
	//Do the work: add user name and data, encrypting the password 
	_AddUser(userName, plainPassword, data); 
									
	//POSTCONDITION of this method (invariants are object-scoped, postconditions are methodscoped) 
	Debug.Assert(GetUserCount() == previousUserCount + 1); 
	
	//INVARIANT check: Also, always end of a method (leave object consistent) 
	Invariant(); 
}
									
private void Invariant(){ //User file cannot get corrupt during the whole execution 
	Debug.Assert(CheckUserFileIntegrity()); 
}
````