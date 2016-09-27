#Session Management

* [Session Management](#session-management)
	* [Active Sessions](#active-sessions)
	
---

<a name="session-management"></a>
##Session Management

<a name="active-sessions"></a>
###Active Sessions

Every system user is able to see his active sessions, as well as IP address from which he is logged in, the [user agent](https://en.wikipedia.org/wiki/User_agent) and time of his last activity for that session.

![Vanguard - Active Sessions](assets/img/active-sessions.png)

By clicking the red "x" button, user can invalidate the selected session, which means that he will be automatically logged out from that device.

>**Note!** Session Management is available **only if** `database` session driver is used by Vanguard. More about sessions drivers can be found [here](configuration.html#session-configuration).