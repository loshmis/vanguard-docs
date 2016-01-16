#User Profile

* [User Profile](#user-profile)
	* [Details](#details)
	* [Avatar](#avatar)
	* [Social Networks](#social-networks)
	* [Authentication](#auth)

---

##User Profile

Every user of the system, no matter what his role is, is able to update his profile. Link to user's profile is available at the top right corner, like it is displayed below:

![Vanguard - Link to User Profile](assets/img/dashboard-profile-ling.png)

###Details

On Profile Details page, users can update their basic informations like First Name, Last Name etc. Also, they are able to update they country from a list of available countries, or to update their birthday using easy bootstrap calendar plugin.

![Vanguard User Profile - Details](assets/img/profile-details.png)

###Avatar

Every user is able to set his avatar photo. By clicking "Change Photo" button below his current avatar, he is able to remove current avatar by clicking _No Photo_, to upload avatar image or to use his [Gravatar](https://en.gravatar.com/) (if there is no Gravatar account attached to his email address, default Gravatar image will be displayed).

![Vanguard User Profile - Avatar Modal](assets/img/profile-avatar-modal.png)

If use is authenticated with some social network (like Facebook, for example) he will be able to select avatars from social network he is authenticated with. In this case, the user was authenticated with Facebook, so he is able to select Facebook avatar and use it within the Vanguard application.

####Uploading Avatar

Uploading avatar is ridiculously easy. After selecting **Upload Avatar** option on modal dialog from above, and selecting the avatar photo,  you are able to zoom the selected photo in and out, and move it around until you are happy with how it looks. 
After putting the image to desired position, and clicking the **Save** button, avatar will be automatically cropped and uploaded to the server, and user's avatar will be updated.

![Vanguard User Profile - Avatar Upload](assets/img/profile-avatar-upload.png)