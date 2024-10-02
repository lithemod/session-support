# Session Support

## Installation

To use the `lithemod/session-support` component in your PHP application, you can install it via Composer. If you don’t have Composer installed, you can download it from [getcomposer.org](https://getcomposer.org/).

### Step 1: Install Composer

If you haven't installed Composer yet, run the following command in your terminal:

```bash
curl -sS https://getcomposer.org/installer | php
```

### Step 2: Add `lithemod/session-support` to Your Project

Navigate to your project directory and run the following command:

```bash
composer require lithemod/session-support
```

This command will download the package and update your `composer.json` file accordingly.

### Step 3: Start a Session

To use the session functionality, make sure to start a PHP session at the beginning of your script:

```php
session_start();
```

## Using the Session Class

The `Session` class provides a simple and intuitive interface for managing session variables in your PHP applications. Below are detailed descriptions of each method along with examples.

### Setting a Session Variable

You can set a session variable using the `put` method. This method accepts the name of the session variable and the value you want to assign.

```php
use Lithe\Support\Session;

Session::put('username', 'john_doe');
```

### Retrieving a Session Variable

To retrieve the value of a session variable, use the `get` method. You can also specify a default value to return if the session variable does not exist.

```php
$username = Session::get('username', 'default_user');
echo $username; // Output: john_doe
```

### Removing a Session Variable

To remove a specific session variable, use the `forget` method. You can pass a single variable name or an array of names to remove multiple variables at once.

```php
Session::forget('username'); // Remove a session variable

// Remove multiple session variables
Session::forget(['username', 'email']);
```

### Destroying All Session Variables

If you need to clear all session variables, you can use the `destroy` method:

```php
Session::destroy(); // Clears all session variables and destroys the session
```

### Checking if a Session Variable Exists

To check if a specific session variable exists, you can use the `has` method. This method can also accept an array of variable names.

```php
if (Session::has('username')) {
    echo 'Username is set.';
} else {
    echo 'Username is not set.';
}

// Check multiple variables
if (Session::has(['username', 'email'])) {
    echo 'Both variables are set.';
}
```

### Regenerating the Session ID

For security reasons, it's often a good practice to regenerate the session ID. Use the `regenerate` method to do this:

```php
Session::regenerate(); // Regenerates the session ID, invalidating the old session
```

### Retrieving the Current Session ID

You can retrieve the current session ID using the `getId` method:

```php
$currentSessionId = Session::getId();
echo $currentSessionId; // Displays the current session ID
```

### Setting a Custom Session ID

If you need to set a custom session ID, you can do this with the `setId` method:

```php
Session::setId('custom_session_id');
```

### Retrieving All Session Variables

To retrieve all session variables as an associative array, use the `all` method:

```php
$allSessions = Session::all();
print_r($allSessions); // Displays all session variables
```

### Magic Methods

You can also use object property syntax to set and retrieve session variables with the magic methods `__set` and `__get`.

```php
// Set a session variable
$session = new Session();
$session->username = 'john_doe'; // Calls Session::put('username', 'john_doe')

// Get a session variable
echo $session->username; // Calls Session::get('username')
```

### Error Handling

If you try to use session methods without starting a session, a `RuntimeException` will be thrown:

```php
try {
    Session::put('key', 'value'); // Will throw exception if session is not active
} catch (RuntimeException $e) {
    echo $e->getMessage(); // Output: The session is not active.
}
```

## Flash Message Support

The `Flash` class allows you to manage flash messages in sessions. Flash messages are used to store temporary information that should be displayed on the next request.

### Setting a Flash Message

You can set a flash message using the `set` method or directly through the property:

```php
use Lithe\Support\Session\Flash;

// Using the set method
Flash::set('success', 'The operation was completed successfully.');

// Using the magic property
$flash = new Flash();
$flash->info = 'Welcome to our website!';
```

### Retrieving a Flash Message

To retrieve a flash message and remove it from the session, use the `get` method or the magic property:

```php
$message = Flash::get('success');
echo $message; // Output: The operation was completed successfully.

// Using the magic property
$infoMessage = $flash->info; 
echo $infoMessage; // Output: Welcome to our website!
```

### Checking for Flash Messages

To check if a flash message exists, use the `has` method:

```php
if (Flash::has('success')) {
    echo 'Success message exists.';
}

// Check multiple flash messages
if (Flash::has(['success', 'info'])) {
    echo 'Both messages exist.';
}
```

### Keeping Flash Messages

If you need to keep a flash message for the next request, use the `keep` method:

```php
Flash::keep('success'); // The success message will be kept for the next request
```

## Security Best Practices

When working with sessions in web applications, follow these security best practices:

- **Use HTTPS**: Always use HTTPS to protect the data transmitted between the server and the client.
- **Regenerate the Session ID**: Whenever a user logs in or changes privileges, regenerate the session ID to prevent session fixation attacks.
- **Timeout Settings**: Implement a timeout for inactive sessions, destroying them after a certain period of inactivity.
- **Secure Storage**: Avoid storing sensitive information in session variables. Use only non-sensitive data and always validate data before using it.

## Final Considerations

This comprehensive guide provides the necessary details for users to effectively implement and manage sessions and flash messages in their PHP applications using the `lithemod/session-support` component. With the recommended practices and the examples provided, you'll be well-equipped to handle session management effectively and securely. If you have any questions or need further assistance, feel free to ask!