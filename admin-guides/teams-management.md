# Teams management

**Teams** in Vectice simplify user management by allowing administrators to group users with similar responsibilities, assign workspace roles efficiently, and streamline collaboration. Designed with enterprise needs, Teams make managing permissions and responsibilities across workspaces intuitive and scalable.

{% hint style="info" %}
Vectice seamlessly integrates with your enterprise SSO/LDAP system for efficient team management.
{% endhint %}

With Teams, you can:

* **Create and manage teams** with unique names and optional descriptions.
* **Enable or disable teams** as needed to fit your organizational needs.
* **View team details** in a user-friendly table, including filters for status, creation date, and creator.
* **Access team-specific insights** such as the number of members, workspaces assigned, creator, and last updated details.
* **Assign teams to workspaces** with predefined roles: **Reviewer**, **Editor**, or **Manager**.
* **Inherit the highest level of rights** when users are assigned roles through multiple teams or individually.
* **Automatically generate activity logs** for key team events like creation, role changes, and workspace assignments.
* **Notify users and workspace managers** when they are added/removed from a team or when a team is assigned/removed from a workspace.

***

## SSO/LDAP Integration

Vectice integrates seamlessly with your enterprise SSO/LDAP system, enabling effortless mapping of organizational structures and automatic synchronization of team memberships and roles for efficient management.

***

## How to configure Teams manually

### Creating a Team

1. Navigate to **Admin settings** > **Manage teams**.
2. Click the **Create Team** button.
3. Provide a unique name and optional description for the team.
4. Add members with roles as **Admin** or **Member** (viewer-type users cannot be added).
5. Save the team to enable it.

### Assigning Teams to Workspaces

1. Go to the **Teams & Members** tab in the workspace settings.
2. Add a team and assign a role: Reviewer, Editor, or Manager.
3. Review permissions to ensure team roles align with workspace needs.

***

## Managing Team Members

* Access team details by clicking the team name in the **Manage Teams** table in your **Admin settings**.
* Add or remove members, ensuring viewer-type users remain excluded.
* Disabled members (e.g., downgraded to viewer role) cannot be re-enabled.
