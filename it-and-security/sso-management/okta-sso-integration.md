# Okta SSO integration

This guide outlines the steps to integrate Okta with Vectice using SAML, focusing on configuring a secure Single Sign-On (SSO) connection.

1. If you are an Admin, go to **Organization Setting** by clicking your profile icon.

<img src="../../.gitbook/assets/Screenshot 2024-01-01 at 10.59.04 AM.png" alt="" data-size="original">

2. Click on the tab **Authentication settings** and click <img src="../../.gitbook/assets/Screenshot 2024-01-01 at 11.10.10 AM.png" alt="" data-size="line">
3. On the SAML Form, enter a name for the connection.

<figure><img src="../../.gitbook/assets/okta-name.png" alt=""><figcaption></figcaption></figure>

4. Click on <img src="../../.gitbook/assets/Screenshot 2024-01-01 at 11.07.11 AM.png" alt="" data-size="line"> to generate your **Redirect URI** and the **Entity ID** that you’ll need in Okta.
5. To prepare the SAML integration, go to **Okta Admin** and select **Applications -> Applications**.                                                                                                 ![](https://lh7-us.googleusercontent.com/DN3s2VQfK0tCKiaekW2kD_FuH_dUsGGZoDYeu8xndn9a3OQkMyMESso83tgXFndpbPZ6E435HhDhtX8pFkovoaI3ls6roDymD3N5zDHoLJXxag3N58HxN388BbeByHiHSzSgDq98avaWIxiBiafqrg)
6.  Create a new SAML 2.0 App integration by selecting **Create App Integration -> SAML 2.0 -> Next**. &#x20;

    <figure><img src="../../.gitbook/assets/Screenshot 2024-01-01 at 11.16.53 AM.png" alt=""><figcaption></figcaption></figure>
7. Set the app name, ‘Vectice’ for example -> check ‘Do not display application icon to users’ -> click Next.&#x20;

{% hint style="info" %}
Currently, logins initiated from Okta are not supported.
{% endhint %}

8. Copy the **Single sign-on URL** and **Audience URI (SP Entity ID)** from Vectice's **Redirect URI** and **Entity ID**, and paste them into the SAML settings in Okta.
9. For **Application username**, choose ‘Email’.  Click **Next** and Finish the creation of the Okta SAML Integration.&#x20;
10. You will arrive in your SAML Integration Page, click on **View** **SAML setup instructions**.&#x20;

    <figure><img src="../../.gitbook/assets/Saml-setup.png" alt=""><figcaption></figcaption></figure>
11. Copy the **Identity Provider Single Sign-On URL** from this Okta page to use in Vectice.&#x20;

    <figure><img src="../../.gitbook/assets/identity-provider.png" alt=""><figcaption></figcaption></figure>
12. In Vectice, go to Organization settings -> Authentication Method and update the 'Single Sign On Service URL' with Okta's value. Select **Enabled** and save.&#x20;

:tada: **You have enabled Okta SSO authentication for Vectice!**

Now, when users log in to Vectice, they will see an option to login with Okta SSO below the password field.

With SSO enabled, you have a few options:

* You can disable password authentication if you want users to only login via SSO
* You can enable the ability for users to automatically receive a Vectice account from their SSO provider (auto-provisioning)
* You can set up the roles in Okta if they want more fine-tuning on this level.
