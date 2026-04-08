# Lab:Add and Manage Users with Linux Commands

## Lab Source

This lab is based on the Google Cybersecurity Professional Certificate training materials.

Original lab reference:
https://www.skills.google/focuses/47128590?parent=lti_session

## Environment

- OS: Debian-based Linux (Virtual Machine)
- Shell: Bash
- User: `analyst`
- Starting Directory: `/home/analyst`
- Privileges: `sudo` required for all tasks

## Why This Matters (Cybersecurity Context)

In a real SOC (Security Operations Center) environment:

- **Authentication** — verifying who a user is — depends on users being properly provisioned in the system.
- Failing to remove departed employees is a common security gap that can be exploited for unauthorized access.
- Assigning users to the correct groups enforces the principle of least privilege, ensuring people only access what they need.

---

## Key Concepts

- **Primary group:** The default group assigned to a user. Files created by the user are owned by this group.
- **Secondary group:** An additional group a user belongs to, granting access to resources owned by that group.
- **`sudo`:** Required for all user management commands since adding, modifying, and deleting users requires root privileges.

---

## Task 1: Add a New User

A new employee joins the Research department with the username `researcher9`.

### Add the User to the System

```bash
sudo useradd researcher9
```

### Add the User to Their Primary Group

```bash
sudo usermod -g research_team researcher9
```

> **Shortcut:** Both steps can be combined into one command at creation time:
>
> ```bash
> sudo useradd researcher9 -g research_team
> ```

---

## Task 2: Assign File Ownership

`researcher9` takes responsibility for `project_r.txt`, currently owned by `researcher2`.

### Transfer File Ownership

```bash
sudo chown researcher9 /home/researcher2/projects/project_r.txt
```

> **Note:** `chown` changes the ownership of a file or directory. You must use `sudo` since you are modifying a file owned by another user.

---

## Task 3: Add the User to a Secondary Group

`researcher9` is now working across both the Research and Sales departments. Their primary group remains `research_team`, but they need to be added to `sales_team` as a secondary group.

```bash
sudo usermod -a -G sales_team researcher9
```

> **Note:** Options are case-sensitive here:
>
> - `-a` (lowercase) — append, so the user is added without being removed from existing groups.
> - `-G` (uppercase) — specifies a supplementary (secondary) group.
>
> Omitting `-a` would replace all existing secondary groups, which could unintentionally revoke access.

---

## Task 4: Delete a User

`researcher9` has left the organization and must be removed from the system.

### Delete the User

```bash
sudo userdel researcher9
```

**Expected Message:**

```
Userdel: Group researcher9 not removed because it is not the primary group of user researcher9.
```

> This message is expected and not an error. When a user is created in Linux, a group with the same name is automatically created. Since `research_team` (not `researcher9`) is their primary group, that auto-created group is left behind and must be cleaned up manually.

### Delete the Leftover Group

```bash
sudo groupdel researcher9
```
