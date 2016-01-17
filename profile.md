#User Profile

* [User Profile](#user-profile)
	* [Details](#details)
	* [Avatar](#avatar)
	* [Social Networks](#social-networks)
	* [Authentication](#auth)

---

<a name="user-profile"></a>
##User Profile

Every user of the system, no matter what his role is, is able to update his profile. Link to user's profile is available at the top right corner, like it is displayed below:

![Vanguard - Link to User Profile](assets/img/link-user-profile.png)

<a name="details"></a>
###Details

On Profile Details page, users can update their basic informations like First Name, Last Name etc. Also, they are able to update they country from a list of available countries, or to update their birthday using easy bootstrap calendar plugin.

![Vanguard User Profile - Details](assets/img/profile-details.png)

<a name="avatar"></a>
###Avatar

Every user is able to set his avatar photo. By clicking "Change Photo" button below his current avatar, he is able to remove current avatar by clicking _No Photo_, to upload avatar image or to use his [Gravatar](https://en.gravatar.com/) (if there is no Gravatar account attached to his email address, default Gravatar image will be displayed).

![Vanguard User Profile - Avatar Modal](assets/img/profile-avatar-modal.png)

If use is authenticated with some social network (like Facebook, for example) he will be able to select avatars from social network he is authenticated with. In this case, the user was authenticated with Facebook, so he is able to select Facebook avatar and use it within the Vanguard application.

####Uploading Avatar

Uploading avatar is ridiculously easy. After selecting **Upload Avatar** option on modal dialog from above, and selecting the avatar photo,  you are able to zoom the selected photo in and out, and move it around until you are happy with how it looks. 
After putting the image to desired position, and clicking the **Save** button, avatar will be automatically cropped and uploaded to the server, and user's avatar will be updated.

![Vanguard User Profile - Avatar Upload](assets/img/profile-avatar-upload.png)

<a name="social-networks"></a>
###Social Networks

Users can, optionally, provide their social networks accounts by updating them on Social Networks tab, inside their Profile page.

 ![Vanguard User Profile - Social Networks](assets/img/profile-socials.png)

Those social networks will be displayed when administrator view their [profile](users/show) from backend.

<a name="auth"></a>
###Authentication

On Authentications tab, under Profile section, every user is able to update his login details including email, username and password. If password field is empty when users click "Update Details" button, password will not be updated.

![Vanguard User Profile - Authentication](assets/img/profile-auth.png)

Users are also able to enable or disable Two-Factor Authentication (2FA) for their account (of course, if it is enabled globally by administrators). And, as it already mentioned in [authentication section](auth#two-factor-token), in order to use two factor authentication, user has to install Authy application on his phone.

In order to enable 2FA, user has to provide his Country Code and Cell Phone number, without country code prefix. For example, if your cell phone number is +12345678, and you are from USA, then your Country Code will be `1` and your Cell Phone Number will be `2345678`.

If you are not sure what your country code is, list of all country codes can be found [here](https://countrycode.org/).

