# Add external user authentication to your web application with the reset password flow
This tutorial shows you how authenticate selected external users with your web application and with optional password reset feature

## Scenario overview. Contoso Books

Contoso Books, Ltd. is a small but growing company that offers digital purchases of books. They were very succesfull by providing an inventory that is comparable to what the larger online book stores offer. Now they would like to provide analytics services to the book publishers interested in the readers reviews for selected books. Publishers interested in the review analytics will submit a list of books they are intersted in through the Contoso publishers Analytics Portal.

Contoso Books wants to manage publisher accounts accessing the Analytics Portal. Publishers should be able to reset their passwords. Contoso Books decided to use [Azure AD B2C](https://docs.microsoft.com/en-us/azure/active-directory-b2c/overview) as the Identity Provider service.

## Setup Azure AD B2C
Login into Azure Portal and create a new Azure AD B2C tenant:
![](docs/media/2022-06-02-16-19-51.png)

![](docs/media/2022-06-02-16-20-35.png)

![](docs/media/2022-06-02-16-21-17.png)

![](docs/media/2022-06-02-16-22-58.png)

![](docs/media/2022-06-02-16-32-58.png)

It will take a few minutes to create a new tenant

Navigate to your new tenant:

![](docs/media/2022-06-02-16-36-07.png)

Create an App Registration for your web application. For the test purposes use https://jwt.ms as the redirect URL

![](docs/media/2022-06-02-16-38-07.png)

![](docs/media/2022-06-02-16-38-38.png)

![](docs/media/2022-06-02-16-40-01.png)

![](docs/media/2022-06-02-16-41-11.png)

Switch back to the AAD B2C blade:

![](docs/media/2022-06-02-16-42-15.png)

Switch to Users to add a new publisher user since we are not providing a public sign-up to our portal:

![](docs/media/2022-06-02-16-45-08.png)

![](docs/media/2022-06-02-16-46-00.png)

Fill in your publisher user data:

![](docs/media/2022-06-02-16-49-40.png)

You will see a new user created:

![](docs/media/2022-06-02-16-51-12.png)

You can reset user password and share it with your publisher

![](docs/media/2022-06-02-17-05-21.png)

Create a new authentication flow for your user from the AAD B2C blade and select User flows:

![](docs/media/2022-06-02-16-53-52.png)

![](docs/media/2022-06-02-16-54-33.png)

Select Sign-in:

![](docs/media/2022-06-02-16-55-19.png)

and "Recommended"

![](docs/media/2022-06-02-16-56-01.png)

Fill in the Flow data:

![](docs/media/2022-06-02-16-58-08.png)

Now you can test your flow:

![](docs/media/2022-06-02-16-58-56.png)

But before that you need to finish the flow configuration:

![](docs/media/2022-06-02-17-00-34.png)

Save and test it (Run user flow):

![](docs/media/2022-06-02-17-01-16.png)

![](docs/media/2022-06-02-17-02-12.png)

The browser will display the authentication challenge:

![](docs/media/2022-06-02-17-02-54.png)

![](docs/media/2022-06-02-17-06-48.png)

The user will be requested to change the password:

![](docs/media/2022-06-02-17-08-00.png)

The password will be changed:

and our test reditect URL (jwt.ms) will return an empty result:

![](docs/media/2022-06-02-17-10-22.png)

Now let's test self-service password reset:

Run the workflow again:

![](docs/media/2022-06-02-17-12-01.png)

![](docs/media/2022-06-02-17-12-24.png)

![](docs/media/2022-06-02-17-13-15.png)

The verification code was sent to your publisher user.

The publisher will open the email:

![](docs/media/2022-06-02-17-16-38.png)

and use the verification code:

![](docs/media/2022-06-02-17-17-49.png)

and continue:

![](docs/media/2022-06-02-17-18-35.png)

new password will be entered:

![](docs/media/2022-06-02-17-19-13.png)

and again empty test jwt.ms content will be displayed.

The user has the right password now and wants finally to authenticate with the application:

Run the user flow again:

![](docs/media/2022-06-02-17-20-59.png)

![](docs/media/2022-06-02-17-21-47.png)

The token is and was empty because we do not set the token usage in the application registration (TODO - need to have it right at the beginning)):

Go the the App Registration/Authentication and change it:

and run the flow again

![](docs/media/2022-06-02-17-27-55.png)

We are still missing Country or Region in the claims. Let's configure it:

![](docs/media/2022-06-02-17-32-04.png)


and run the flow again:

![](docs/media/2022-06-02-17-33-54.png)

let's also add the user email address to the claims:

![](docs/media/2022-06-02-17-35-14.png)

and run the flow again:

![](docs/media/2022-06-02-17-35-25.png)

![](docs/media/2022-06-02-17-37-30.png)

our next step will be to configure our Analytics Portal instead of jwt.ms so that the claims will be used by the application after the authentication.





