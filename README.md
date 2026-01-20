# Part 2 - Active Directory Setup Lab 

This repository documents a hands-on **Active Directory Domain Services (AD DS)** lab completed in Microsoft Azure. The lab demonstrates installing Active Directory, promoting a Domain Controller, creating administrative users and organizational units, and joining a client machine to the domain.

This environment will be reused for future labs (Group Policy, user management, security hardening, and help desk integration).

---

## 🖥️ Environment

| Component           | Description                        |
| ------------------- | ---------------------------------- |
| DC-1                | Windows Server (Domain Controller) |
| Client-1            | Windows Client VM                  |
| Platform            | Microsoft Azure                    |
| Domain              | `company.com` (customizable)      |
| Initial Local Admin | `labuser`                          |

---

## Install Active Directory Domain Services

### 1. Log in to DC-1

Log in to the server using the local administrator account: `labuser`

---

### 2. Install AD DS Role

1. Open **Server Manager**
2. Select **Add roles and features**
3. Proceed to **Server Roles**
4. Select **Active Directory Domain Services**
5. Complete the wizard and install

---

### 3. Promote Server to Domain Controller

1. In **Server Manager**, click the notification flag
2. Select **Promote this server to a domain controller**
3. Choose **Add a new forest**
4. Set the root domain name: `company.com`

5. Complete the wizard using default settings
6. Allow the server to restart

---

### 4. Log in Using Domain Credentials

After reboot, log back into DC-1 using: ` company.com\labuser` or `labuser@company.com`

---

## Part 2: Create Domain Admin User & OUs

### 1. Open Active Directory Users and Computers (ADUC)

Navigate to:

```
Start → Administrative Tools → Active Directory Users and Computers
```

---

### 2. Create Organizational Units

Under the domain (`company.com`), create the following OUs:

* `_EMPLOYEES`
* `_ADMINS`

---

### 3. Create a Domain Admin User

Create a new user in the `_ADMINS` OU with the following details:

| Field    | Value          |
| -------- | -------------- |
| Name     | Jane Doe       |
| Username | `jane_admin`   |
| Password | `Cyberlab123!` |

---

### 4. Add User to Domain Admins Group

1. Right-click `jane_admin`
2. Select **Properties**
3. Open the **Member Of** tab
4. Add the **Domain Admins** group
5. Apply changes

---

### 5. Log in as Domain Admin

Log out of DC-1 and log back in using:

```
company.com\jane_admin
```

✅ From this point forward, `jane_admin` is used as the primary administrative account.

---

## Part 3: Join Client-1 to the Domain

### 1. Verify DNS Settings (Azure)

* Client-1 DNS is configured to use DC-1’s **private IP address**
* Client-1 has been restarted via the Azure Portal

---

### 2. Join Client-1 to Domain

1. Log in to Client-1 as:

```
labuser
```

2. Open **System Properties**
3. Select **Change settings** → **Change**
4. Choose **Domain** and enter:

```
company.com
```

5. Authenticate using: `company.com\jane_admin` or `jane_admin@company.com`

6. Restart when prompted

---

### 3. Verify Client in Active Directory

1. Log into DC-1 as `jane_admin`
2. Open **Active Directory Users and Computers**
3. Confirm **Client-1** appears in the **Computers** container

---

### 4. Organize Client Computers

1. Create a new OU named:

```
_CLIENTS
```

2. Move **Client-1** into the `_CLIENTS` OU

---

