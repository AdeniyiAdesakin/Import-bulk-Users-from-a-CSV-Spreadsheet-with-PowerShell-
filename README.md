<h3>*Import bulk Users from a CSV Spreadsheet with PowerShell </h3>
<p>1. To import bulk users into an OU from a CSV Spreadsheet with powershell. First,I prepared an excel sheet with all the user’s attributes and save it as a csv file. </p>
<p align="center"><img src="https://i.imgur.com/QjdS8HT.png" height="50%" width="50%" alt="image"/>

<p>2. Open up Windows Powershell and Import  Import active directory module for running AD cmdlets by running this command <b><i>“Import-Module activedirectory”</i></b>. Also, Import the users from the path I stored the files in ADUser variable by running this command <b><i>“ $ADUsers = Import-csv C:\Bulk\Edmontonusers.csv”</i></b>.</p>
<p align="center"><img src="https://i.imgur.com/1gNzPXy.png" height="50%" width="50%" alt="image"/>

<p>3. Now to create the users in the specified OU on the Spreadsheet, I ran these commands <b><i>“ foreach ($User in $ADUsers)
{#Read user data from each field in each row and assign the data to a variable as below
$Username 	= $User.username
$Password 	= $User.password
$Firstname 	= $User.firstname
$Lastname 	= $User.lastname
$OU 		= $User.ou #This field refers to the OU the user account is to be created in
 $email      = $User.email
$streetaddress = $User.streetaddress
$city       = $User.city
$zipcode    = $User.zipcode
$state      = $User.state
$country    = $User.country
$telephone  = $User.telephone
$jobtitle   = $User.jobtitle
$company    = $User.company
$department = $User.department
$Password = $User.Password
#Check to see if the user already exists in AD
if (Get-ADUser -F {SamAccountName -eq $Username})
{#If user does exist, give a warning
Write-Warning "A user account with username $Username already exist in Active Directory."
	}
	else
	{
#User does not exist then proceed to create the new user account
 #Account will be created in the OU provided by the $OU variable read from the CSV file
New-ADUser `
    -SamAccountName $Username `
  -UserPrincipalName "$Username@adeniyi.com" `
 -Name "$Firstname $Lastname" `
 -GivenName $Firstname `
 -Surname $Lastname `
-Enabled $True `
-DisplayName "$Firstname $Lastname" `
-Path $OU `
 -City $city `
 -Company $company `
 -State $state `
 -StreetAddress $streetaddress `
 -OfficePhone $telephone `
 -EmailAddress $email `
 -Title $jobtitle `
  -Department $department `
 -AccountPassword (convertto-securestring $Password -AsPlainText -Force) -ChangePasswordAtLogon $true
          	}
}</i></b> </p>
<p align="center"><img src="https://i.imgur.com/DLHA327.png" height="50%" width="50%" alt="image"/>

<p>4. Back to the Active Directory Users and Computers, click on Edmonton OU and refresh it to see if the users are there and there they are</p>
<p align="center"><img src="https://i.imgur.com/2AWpZao.png" height="50%" width="50%" alt="image"/>



<br>
