# Sessions

## Cookies

Cookies are small pieces of data that websites store on your browser. They are used to remember information about you, such as your login credentials and preferences. Vectice is securing your cookies through HttpOnly, Secure, and SameSite attributes.

### HttpOnly

This attribute restricts access to the cookie's content. With HttpOnly enabled, scripts running on a webpage (like JavaScript) cannot access the cookie's value. This is important because malicious scripts could potentially steal cookie data if it were accessible through JavaScript.

### Secure

This attribute ensures the cookie is only transmitted over HTTPS connections. Regular HTTP connections are unencrypted, making them vulnerable to eavesdropping. By setting the Secure attribute, the cookie is only sent when the browser communicates with the website over a secure HTTPS connection.

### SameSite

This attribute controls when the browser sends the cookie and requests to the same website or different websites.

## Session timeout

Keycloak is used to manage session timeouts to ensure your account security. We understand that protecting your data is paramount, and Keycloak employs several mechanisms to achieve this:

{% hint style="info" %}
Values for the following parameters can be customized to match your needs.
{% endhint %}

* **Idle session:** Expires after inactivity to prevent unauthorized access on unattended devices.
* **Maximum session lifespan:** Enforces a session expiration regardless of activity for added security.
* **Access token lifespan:** Limits the validity of tokens used by applications to minimize risk from breaches.

## API keys

API keys are secret credentials applications use to access resources on your behalf. Here's how we ensure their security:

* **Deactivation:** Disable compromised or unused API keys to regain control and prevent access.
* **Storage:** On the Vectice side, API Keys are signed using the HMAC algorithm before being stored in the Database.
* **Security best practices:**
  * **Rotation:** Regularly rotate your API keys to minimize the risk associated with a compromised key remaining active for an extended period. Think of it like changing your passwords – it reduces the window of vulnerability.
  * **Store securely:** Never share your API keys publicly or store them in plain text. Use secure methods like password managers for safekeeping. Treat them like valuable keys to your digital resources.
