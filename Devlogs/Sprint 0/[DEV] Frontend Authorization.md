## **Research Devlog - Frontend Authorization**

This devlog will describe the process of the implementation of Authorization into the frontend of the Van den Bosch AMS assignment.
#

## Challenge
*How do we effectively identify users without the annoyance of constant sign-in's?*

The AMS project created for this assignment is meant to be an internal tool for employees. This means that we need to be able to identify users and determine wether said user belongs to the company, and only then give them access. However, we also dont want to constantly bother the user with identifiying themselves every time they do something. This brings up the question, how do we identify our users in an effective way without constant sign-in's?  

<br><br>

## Solution
To determine what solutions for identifying users could be used I will first look into how other platforms within the company do so, mainly Workspace365 (Digital working environment), Tengio (An in-house employees platform) and Lunch e-shop.

### Workspace365
Workspace365 uses the companies login system of Microsoft Azure's Active Directory coupled to the employee accounts in the Azure environment. This means that every employee can log in through their employee acount and make use of this service through that.

### Tengio
Tengio at first site does not appear to have any login identification: When going to the site the user is not requested any login details. However, the site does actually log you into an account of your own, linked to the employee. Later in a conversation with my internship coach it was determined this was done through Active Directory Single Sing On.

### Lunch e-shop
Lunch e-shop uses an account that the user makes themselves on going onto the site for the first time. This means the accounts are not directly linked to the employees, but instead are loose entities.

<img src="https://ictresearchmethods.nl/images/8/87/Logo-library.png" width="25px" /> *Library, existing solutions*

<br>

Next up I talked with my internship coach, who is also the primary group of users for the application, on what type of identification would be applicable, both from a requirement standpoint and a user interaction standpoint. 

I mainly asked what method he would like to see on an internal application. He suggested looking into Active Directory's Single Sign On method which would make signing in with the employees company account possible, but would also mean the employee would automatically be logged in if they already have logged in on a different site that also uses the Single Sign On.

<img src="https://ictresearchmethods.nl/images/d/d4/Logo-field.png" width="25px" /> *Field, user research*

<br><br>

## Result
As a result of the above mentioned findings I decided to implement the Azure Active Directory Single Sign On approuch in my platform. However, this posed one major problem: To implement this system, a developer key for the Active Directory is required which needs to be requested at the IT departement and is not likely to be issued.

This was discussed with my internship coach and together we came to a conclusion to move the use of the Active Directory down in priority. Instead I looked for a solution that offers standalone user identification but is also relatively easy to swap out with Active Directory Authorization later on.

<br>

Looking around online at platforms that offer this standalone service came up with Auth0. The positive side of using Auth0 is that it has built-in support for use of Active Directory sign in meaning that codewise no changes need to be made to later on implement this into the application. Thus I chose Auth0 for main Authorization service for my applications.

| Auth0 Sign in page | Auth0 users |
| :--- | :--- |
| ![Auth0 Login](../../Media/Auth0%20login.png) | ![Auth0 Users](../../Media/Auth0%20users.png) |

<br><br>

## Validation
To validate that this sign on method is indeed what users want to see, the Active Directory integration first has to happen. However, because the developer keys required for this are not available yet, this validation cannot yet happen, and will have to be done at a later date. This willl be done in the form of user testing where I ask a handful of users to try using the site witout telling them I'm investigating the sign-in process, and then collect their experience with the sign-in afterwards.

<img src="https://ictresearchmethods.nl/images/a/ac/Logo-lab.png" width="25px" /> *Lab, user testing*

<br><br>

## Next
Up next I will implement the Active Directory sign on so users can sign in with their employee accounts once the developer keys are avaible, and will then also do validation of the result as described in the 'Validation' section.