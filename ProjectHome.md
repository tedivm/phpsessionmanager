This project contains the code from [this blog post](http://carsonified.com/blog/dev/how-to-create-bulletproof-sessions/) on [Carsonified](http://carsonified.com/blog).

**Updated 9/24/09**

## Usage ##

Starting the session is a simple call to the "sessionStart" static function.

```
// Creates a basic session.
SessionManager::sessionStart('InstallationName');

// Creates a session thats ends when the browser closes and is only accessible at www.site.com/myBlog/
SessionManager::sessionStart('Blog_myBlog', 0, '/myBlog/', 'www.site.com');

// Creates a session thats ends when the browser closes and is only accessible at https://accounts.bank.com/
SessionManager::sessionStart('Accounts_Bank', 0, '/', 'accounts.bank.com', true);
```

You can manually set a session id to regenerate using the regenerateSession function. This is useful for when you change authentication states (the user logs in or out) as it also invalidates the old session.

```
// Regenerate the session.
SessionManager:: regenerateSession();
```

## Features ##

  * Protects against fixation attacks by regenerating the ID periodically.
  * Prevents session run conditions caused by rapid concurrent connections (such as when Ajax is in use).
  * Locks a session to a user agent and ip address to prevent theft.
  * Supports users behind proxies by identifying proxy headers in requests.
  * Handles edge cases such as AOL's proxy network and IE8's user-agent changes.