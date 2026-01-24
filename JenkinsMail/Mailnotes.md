# Jenkins Email & Mailer Plugin – Complete Notes

**WHAT IS PLUGINS :**
Plugins in Jenkins are add-ons that extend its core functionality

Jenkins is light  weight with help help of plugins its been strong
support with 
```bash
like github,Docker,notification,diff build Tooland UI improvement\
```
Plugins is new Enhancement to Jenkins



## 1. Introduction

Jenkins provides **email notification** features to inform users about job build status (SUCCESS / FAILURE / UNSTABLE). This is achieved using:

* **Mailer Plugin** (Basic email notification)
* **Email Extension Plugin (Email-ext)** (Advanced & customizable email notification)

These plugins allow Jenkins to send emails when a build fails, succeeds, or changes status.

---

## 2. Plugins Overview

### 2.1 Mailer Plugin

* Comes **pre-installed** with Jenkins in most cases
* Used for **simple email notifications**
* Limited customization

### 2.2 Email Extension Plugin (Email-ext)

* Must be **installed manually**
* Supports:

  * HTML emails
  * Attachments
  * Triggers (failure, success, unstable, aborted, etc.)
  * Dynamic email content

👉 **Recommended**: Use **Email Extension Plugin** for real projects.

---

## 3. Plugin Installation

### Steps to Install Plugins

1. Go to **Jenkins Dashboard**
2. Click **Manage Jenkins**
3. Select **Manage Plugins**
4. Open **Available** tab
5. Search for:

   * `Email Extension Plugin`
   * `Mailer Plugin` (if not already installed)
6. Select plugins
7. Click **Install without restart** (or restart Jenkins if required)

---

## 4. Configure Email in Jenkins (Global Configuration)

### Navigate to System Configuration

1. Jenkins Dashboard → **Manage Jenkins**
2. Click **System**
3. Scroll to **E-mail Notification** section

---

## 5. Configure Mailer Plugin (Basic Email)

### Settings

* **SMTP Server**: `smtp.gmail.com`
* **Default user e-mail suffix**: `@gmail.com` (optional)
* **Use SMTP Authentication**: ✔

  * Username: `your_email@gmail.com`
  * Password: `App Password` (NOT normal Gmail password)
* **Use SSL**: ✔
* **SMTP Port**: `465`
* **Reply-To Address**: your email
* **Charset**: `UTF-8`

### Test Configuration

* Click **Test configuration by sending test e-mail**
* Enter your email ID
* Verify email is received

---

## 6. Configure Email Extension Plugin (Advanced)

### Navigate to Email-ext Section

In **Manage Jenkins → System**, scroll to:

### ✉ Extended E-mail Notification

#### Required Settings

* **SMTP Server**: `smtp.gmail.com`
* **SMTP Port**: `465`
* **Use SSL**: ✔
* **SMTP Username**: `your_email@gmail.com`
* **SMTP Password**: `App Password`
* **Default Content Type**: `text/html`
* **Default Subject**:

  ```
  Build ${BUILD_NUMBER} - ${JOB_NAME} - ${BUILD_STATUS}
  ```
* **Default Content**:

  ```
  Job Name: ${JOB_NAME}
  Build Number: ${BUILD_NUMBER}
  Build Status: ${BUILD_STATUS}
  Build URL: ${BUILD_URL}
  ```

#### Save configuration

---

## 7. Gmail App Password Configuration (Important)

Since Google blocks less secure apps:

1. Go to **Google Account Settings**
2. Enable **2-Step Verification**
3. Go to **App Passwords**
4. Select:

   * App: Mail
   * Device: Other (Jenkins)
5. Generate password
6. Use this password in Jenkins SMTP configuration

---

## 8. Configure Email in Jenkins Job (Builder Configuration)

### Job Level Email Configuration

1. Open Jenkins Job
2. Click **Configure**
3. Scroll to **Post-build Actions**

---

## 9. Using Mailer Plugin in Job

### Steps

1. Click **Add post-build action**
2. Select **E-mail Notification**
3. Configure:

   * **Recipients**: `user1@gmail.com,user2@gmail.com`
   * ✔ Send e-mail for every unstable build
   * ✔ Send e-mail for every failed build

👉 This sends **simple emails** when build fails.

---

## 10. Using Email Extension Plugin in Job (Recommended)

### Steps

1. Click **Add post-build action**
2. Select **Editable Email Notification**

### Configuration

#### Project Recipient List

```
user1@gmail.com,user2@gmail.com
```

#### Subject

```
❌ Build Failed: ${JOB_NAME} #${BUILD_NUMBER}
```

#### Content

```
Hello Team,

The Jenkins build has FAILED.

Job Name   : ${JOB_NAME}
Build No   : ${BUILD_NUMBER}
Status     : ${BUILD_STATUS}
Triggered By: ${CAUSE}

Check console output here:
${BUILD_URL}

Thanks,
Jenkins
```

---

## 11. Configure Email Trigger for Build Failure

### Add Trigger

1. Inside **Editable Email Notification**
2. Click **Add Trigger**
3. Select **Failure**

### Failure Trigger Settings

* **Send To**: `Recipient List`
* (Optional) Override subject/content

👉 Email will be sent **only when build fails**

---

## 12. Common Jenkins Email Variables

| Variable           | Description          |
| ------------------ | -------------------- |
| ${JOB_NAME}        | Job name             |
| ${BUILD_NUMBER}    | Build number         |
| ${BUILD_STATUS}    | SUCCESS / FAILURE    |
| ${BUILD_URL}       | Jenkins build URL    |
| ${CAUSE}           | Build trigger reason |
| ${DEFAULT_CONTENT} | Default email body   |

---

## 13. Troubleshooting Email Issues

### Common Problems

❌ Email not received

* Check SMTP credentials
* Use **App Password** only
* Verify firewall/network access

❌ Authentication failed

* Wrong password
* 2FA not enabled in Gmail

❌ Port issues

* SSL → 465
* TLS → 587

---

## 14. Best Practices

* Always use **Email Extension Plugin**
* Use **HTML email format** for clarity
* Send emails only on **FAILURE / UNSTABLE**
* Avoid spamming on SUCCESS
* Use Jenkins variables for dynamic data

---

## 15. Summary

✔ Install Mailer + Email Extension plugins
✔ Configure SMTP in **Manage Jenkins → System**
✔ Use **Editable Email Notification** in jobs
✔ Add **Failure trigger**
✔ Emails sent automatically when build fails

---

✅ This setup ensures users receive email alerts whenever a Jenkins build fails.
