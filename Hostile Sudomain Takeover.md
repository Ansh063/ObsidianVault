Hostile Subdomain Takeover**

Let’s say a company owns the main domain: `company.com`

And they also have subdomains like:

- `blog.company.com`
    

- `shop.company.com`
    

- `app.company.com`
    

Now imagine that `blog.company.com` used to point to a third-party service like Medium, Heroku, GitHub Pages, or AWS S3. But later, they stopped using that service — **but forgot to remove the DNS entry** (the CNAME record) for `blog.company.com`.

What happens now?

- **DNS still points to Medium**, but the Medium blog is deleted.
    

- An attacker notices this and **creates their own Medium blog** and **claims the same hostname (**`**blog.company.com**`**)**.
    

- Now, when someone visits `blog.company.com`, they see the attacker’s content, **but it still looks like it belongs to the company.**
    

#### [](https://app.gitbook.com/o/zCQP7R342Y3kXbCAn4gU/s/xu0gd8h18Gx3ptcOiG21/offensive-bug-bounty-hunter-2.0/hostile-sudomain-takeover#why-its-dangerous)Why it's dangerous:

- It can be used to **host phishing pages** under the company’s domain.
    

- **Steal credentials**, distribute malware, or harm the company’s reputation.
    

- Since it’s a **valid subdomain**, many users and systems will trust it automatically.
    

---

#### [](https://app.gitbook.com/o/zCQP7R342Y3kXbCAn4gU/s/xu0gd8h18Gx3ptcOiG21/offensive-bug-bounty-hunter-2.0/hostile-sudomain-takeover#visual-example)Visual Example:

|||
|---|---|
|`blog.company.com` → Medium|Medium blog is deleted|
|Attacker registers same Medium blog|Now controls `blog.company.com`|

---

#### [](https://app.gitbook.com/o/zCQP7R342Y3kXbCAn4gU/s/xu0gd8h18Gx3ptcOiG21/offensive-bug-bounty-hunter-2.0/hostile-sudomain-takeover#how-attackers-find-this)How attackers find this:

- Use tools like `Subjack`, `Takeover`, or `Amass` `Sublist3r` to find subdomains.
    

- Check if the DNS points to known third-party services.
    

- See if the resource is **unclaimed** or **decommissioned**.
    

---

#### [](https://app.gitbook.com/o/zCQP7R342Y3kXbCAn4gU/s/xu0gd8h18Gx3ptcOiG21/offensive-bug-bounty-hunter-2.0/hostile-sudomain-takeover#real-world-checks)Real World Checks:

- Run: `dig blog.company.com`
    

- If it resolves to GitHub Pages but no content loads, it might be vulnerable.
    

- The attacker signs into GitHub, creates a repo, links it — and boom — takeover.
    

---

#### [](https://app.gitbook.com/o/zCQP7R342Y3kXbCAn4gU/s/xu0gd8h18Gx3ptcOiG21/offensive-bug-bounty-hunter-2.0/hostile-sudomain-takeover#fix)Fix:

- Regularly audit DNS records.
    

- Remove CNAME entries that point to **unused third-party services**.
    

- Set up **monitoring tools** to catch takeovers early.
![[Pasted image 20250904125523.png]]

