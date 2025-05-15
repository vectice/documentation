# CORS/CSRF

Cross-origin resource sharing (CORS) and Cross-site request forgery (CSRF) are web security mechanisms dealing with different aspects of web requests.

**Here's the key difference:**

* **CORS** deals with access control between origins for resource sharing.
* **CSRF** focuses on preventing unauthorized actions by a logged-in user of the same origin.

## Robust security at Vectice: CORS, Secure cookies, and Keycloak

At Vectice, we implement a multi-layered approach to ensure your information remains protected, including:

* **CORS best practices:** We enforce Cross-origin resource sharing (CORS) best practices. This restricts how web pages from other domains can interact with our resources, helping to prevent unauthorized access attempts.
* **Secure cookies:** We leverage cookies to manage user sessions. These cookies are[ configured with the `SameSite` attribute](../sessions.md), which mitigates the risk of certain types of attacks, including Cross-site request forgery (CSRF) attacks.
* **Keycloak integration:** We utilize Keycloak, a robust identity and access management (IAM) solution for added security. Keycloak implements robust CSRF protection mechanisms through the use of CSRF tokens. These tokens are unique values embedded in forms or requests that the server validates. This prevents attackers from forging requests that could leverage your authenticated session.

This combined approach provides comprehensive protection against unauthorized access to your data. By implementing CORS best practices, secure cookies, and Keycloak's CSRF protection, we strive to create a secure environment for your information.
