#Authentication & Registration

* [Authentication & Registration](#authentication-and-registration)
	* [Logging In](#logging-in)
	* [Two-Factor Token](#two-factor-token)
	* [Registration](#registration)
	* [Password Reset](#password-reset)

---

<a name="authentication-and-registration"></a>
##Authentication & Registration

<a name="logging-in"></a>
###Logging In

After accessing any Vanguard-protected URL, user will automatically be redirected to the Login Page.  Users are able to log in by typing their username (or email) and password, or by using some of Social Authentication options (if enabled). Login form is displayed below:

![Vanguard - Login Form](assets/img/login.png)

<a name="two-factor-token"></a>
###Two-Factor Token

If Two-Factor Authentication is enabled for specific user, after entering correct username/email and password combination, he will be redirected to Two-Factor Token page displayed below, to enter [Authy](https://www.authy.com/) 2FA token. This means that user has to download secure [Authy app](https://www.authy.com/app/) on his mobile phone and use the token value available upon application installation.

![Vanguard - Two-Factor Authentication Form](assets/img/2fa-token.png)

After entering the 2FA token, Vanguard will contact Authy servers to check the token value, and, **only** if token is correct, user will be logged in.

<a name="registration"></a>
###Registration

Since registration can be completely disabled inside [application settings](settings.html#auth), registration form is only accessible if registration is enabled.

Users are able to access the registration form and create new account by clicking the **Don't have an account?** link on login page and filling up the registration form.

![Vanguard - Registration Form](assets/img/registration.png)

If it is enabled inside application settings, user also has to confirm that they are humans by passing Google reCAPTCHA test.

After successful registration, depending on application settings, user has to confirm their email address if they want to log in for the first time. If email confirmation is disabled by system administrator, users will be able to login right after successful registration.

<a name="password-reset"></a>
###Password Reset

In case that some user forgot his password, he will be able to reset it from Forgot Password form available, after clicking **I forgot my password** link on login page.

![Vanguard - Link to Forgot Password Form](assets/img/login-password-remind.png)

![Vanguard - Forgot Password Form](assets/img/password-remind.png)

>**Note!** Password reset page is accessible only if that option is enabled by system administrator.

After filling in the email used for that account, user will receive an password reset email with a password reset link. That link will be available for a predefined period of time, which is, again, defined by system administrators inside application settings.

When user click on received password reset link, password reset form will be displayed and it will allow them to enter their new password.

![Vanguard - Password Reset Form](assets/img/password-reset.png)
