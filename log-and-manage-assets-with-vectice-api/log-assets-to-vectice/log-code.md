# Log code

Vectice logs your `git` commit information, including the repository name, branch name, commit hash, and the commit URL when there is a `.git` folder or repository available. **Only** locally changed files not logged in Vectice are logged with each **new** git commit.

{% hint style="info" %}
Vectice is **not** a substitute for a code versioning system and is best used in coordination with a git-based system.
{% endhint %}

## Prerequisites&#x20;

To log code in Vectice, you will need the following prerequisites:

* Ensure you have [installed vectice](../connect-to-api.md#install-vectice) with the correct version
* Configure your API to [connect to the Vectice API ](../connect-to-api.md)
* Locally configure your Git username and user email
* Check out a git branch
* Add a valid remote (origin)
* Make at least one commit

### Git configuration

{% hint style="info" %}
Vectice supports all `git` integrations, including **GitHub**, **GitLab**, and **Bitbucket**.
{% endhint %}

You can obtain the prerequisites by first configuring your environment with your `Git` user name and email via the `Git CLI`.

```bash
git config --global user.name "My Name"
git config --global user.email "my@email.com"
```

Then, either clone your existing remote repository or create a new one, followed by adding a valid remote origin.

```bash
git clone https://github.com/user/repo # Clone repo 
```

```bash
git init . # New repo
git remote add origin https://github.com/user/repo # Adding a valid remote origin
```

Lastly, make your first commit to begin code capture.&#x20;

```bash
git add "README.md" # or some other file
git commit -m "Initial commit"
```

{% hint style="info" %}
Commits may not include the latest code changes in the Vectice app. Ensure to commit all new code changes.&#x20;
{% endhint %}

## Code capture overview

**Automatic code capture is enabled by default,** and it happens when:

* You push a new commit with code changes that are not already logged
* You [log a model ](log-models.md)within an iteration
* You [log a dataset](log-datasets.md) (origin, cleaned, or modeling datasets) within an iteration

{% hint style="info" %}
More than one capture can happen within a single iteration.
{% endhint %}

With automatic code capture **enabled**, you will see the following **log output** indicating successful code capture:

```bash
Code captured the following changed files; <filename>.txt, <anotherfilename>.txt
```

In the Vectice app, you can view the `git` branch and the commit hash. You can click the `git` hash or **View** to see your code changes in your repository.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-02-07 at 10.24.28 AM.png" alt=""><figcaption></figcaption></figure>

## Disable code capture

To **disable** the automatic capture of your local code, you can set `code_capture` to `False`, as shown below. Ensure to set this method at the **global** level.

<pre class="language-python"><code class="lang-python"><strong>import vectice
</strong><strong>vectice.code_capture = False
</strong></code></pre>

## Code capture best practices

* Don't forget to **commit your code before running your iteration** so that you log a clean commit into Vectice.
* Work in a separate branch for each experiment to make it easy to reproduce the work and track changes.
* Ensure to **commit your final code changes before completing an iteration** to ensure all the latest commits are logged in the Vectice app.
