## What is Broken access controls

**Broken access controls** are a common and serious security issue. Setting up and managing access controls is complicated because it needs to follow business rules, company structure, and legal requirements. Since people make these decisions, mistakes can easily happen, which can lead to security problems.

**Vertical privilege escalation** happens when a user gets access to features or actions they shouldn’t have — usually more powerful ones. For example, if a regular user can open an admin page and delete accounts, that’s vertical privilege escalation.

## Unprotected functionality

**Vertical privilege escalation** happens when an app doesn’t properly protect sensitive features. For example, admin tools might only be shown to admins on their page, but if a regular user manually types in the admin URL (like `https://insecure-website.com/admin`), they might still be able to access it.

Sometimes, admin links can be found in files like `robots.txt`, or hackers can guess these URLs using word lists. If the site doesn’t check who is allowed to access the page, anyone could get in — which is a big security flaw.

Sometimes, websites try to **hide sensitive features** (like admin pages) by using hard-to-guess URLs — this is called **"security by obscurity"**. For example:

`https://insecure-website.com/administrator-panel-yb556

This might seem safe because the link looks random, but it's **not real security**. Attackers can still find the hidden URL in different ways — like in JavaScript code.

For instance, even if a user isn’t an admin, they can still see the JavaScript that builds the admin link:

```JS
var isAdmin = false; if (isAdmin) {    var adminPanelTag = document.createElement('a');    adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');    adminPanelTag.innerText = 'Admin panel'; }
 ```

So even though the link is only shown to admins in the UI, **anyone can read the code and find the link**, which defeats the purpose of hiding it.

## Parameter-based access control methods

Some websites decide what a user can access (like admin or regular user) during login and store that info in places **users can change**, such as:

- Hidden form fields
    
- Cookies
    
- URL parameters (like `?admin=true`)

For example:

```URL
https://insecure-website.com/login/home.jsp?admin=true  
https://insecure-website.com/login/home.jsp?role=1

```

This is **insecure** because users can change these values and pretend to be admins — gaining access to things they shouldn't. Relying on user-controlled data for access control is a big mistake.

## Horizontal Privilege Escalation (HPE)

This happens when a user can access **another user's data or actions** — instead of just their own.

**Example: 

A user goes to their account page:

```bash
https://insecure-website.com/myaccount?id=123

```
If they change the ID to `id=124`, and it shows **another user's account**, that’s horizontal privilege escalation.

This is usually due to an **IDOR vulnerability** (Insecure Direct Object Reference), where the app directly uses values like `id=123` without checking if the user is allowed to access that specific data.

---

### What about GUIDs?

Some apps use **non-guessable values** like:

```bash 
?id=b7e45fae-3a22-4c67-b123-91b0fd52a0ae

```



This is more secure, but **still risky**. If GUIDs are leaked elsewhere (like in reviews, messages, or URLs), attackers might still use them to access unauthorized data.


## Horizontal to Vertical Privilege Escalation**

Sometimes, a **horizontal attack** (accessing another user’s account) can lead to a **vertical attack** (gaining admin powers).

***Example: 

An attacker changes a URL like:

```bash
https://insecure-website.com/myaccount?id=456

```

If user `456` is an **admin**, the attacker might now:

- See the admin’s private info
    
- Change their password
    
- Access admin-only features
    

This means the attacker went from being a normal user to acting like an **admin**, by first exploiting horizontal access and then turning it into **vertical privilege escalation**.
