# Jenkins – Creating a Freestyle Job (Step-by-Step Notes)

> **Purpose:** This document explains **how to create a Jenkins Job (Freestyle Project)** from scratch, with clear steps, field explanations, and notes. Suitable for **beginners** and **interview preparation**.

---

## 1️⃣ Open Jenkins Dashboard

1. Open browser
2. Go to Jenkins URL:

   ```
   http://<jenkins-server-ip>:8080
   ```
3. Login with Jenkins credentials

✅ You will see the **Jenkins Dashboard**

---

## 2️⃣ Click on "New Item"

* On the **left-side menu**, click:

  👉 **New Item**

This is used to create a **new Jenkins Job**.

---

## 3️⃣ Enter Job Name

### 🔹 Field: *Enter an item name*

Example Job Names:

* `sample-build-job`
* `springboot-freestyle-build`
* `demo-ci-job`

📌 **Best Practices for Job Name:**

* Use lowercase
* Avoid spaces (use hyphen `-` or underscore `_`)
* Name should reflect purpose of the job

✅ Example:

```
springboot-freestyle-job
```

---

## 4️⃣ Choose Job Type

Select:

👉 **Freestyle project**

### Why Freestyle?

* Easy to configure
* No coding required
* Best for beginners
* UI-based steps

📌 **Note:**
Pipeline is used for advanced CI/CD. Freestyle is best to start learning Jenkins.

---

## 5️⃣ Click "OK"

After entering:

* Job Name
* Selecting **Freestyle project**

👉 Click **OK**

You will be redirected to **Job Configuration Page**.

---

# 6️⃣ Job Configuration Page – Detailed Explanation

---

## 🔹 General Section

### ✔ Description

Enter purpose of the job.

Example:

```
This job is used to build and test the Spring Boot application using Jenkins Freestyle project.
```

📌 **Why Description is Important?**

* Helps team members understand job purpose
* Useful during audits and handovers

---

### ✔ Discard Old Builds (Optional)

✔ Check **Discard old builds**

Fill:

* **Max # of builds to keep:** `10`
* **Max # of days to keep builds:** `7`

📌 Prevents Jenkins disk space issues

---

## 🔹 Source Code Management (SCM)

### Option 1: No SCM

* If you are not using Git

### Option 2: Git (Commonly Used)

✔ Select **Git**

Fill details:

* **Repository URL:**

  ```
  https://github.com/username/project-name.git
  ```

* **Credentials:**

  * Add Git username/password or token

* **Branch Specifier:**

  ```
  */main
  ```

  or

  ```
  */master
  ```

📌 Jenkins will pull code from Git during build

---

## 🔹 Build Triggers

Choose when the job should run:

### Common Options:

✔ **Build manually**

* Default (no trigger selected)

✔ **GitHub hook trigger for GITScm polling**

* Auto build on code push

✔ **Poll SCM**

* Example schedule:

  ```
  H/5 * * * *
  ```

✔ **Build periodically**

* Example (every night at 12 AM):

  ```
  0 0 * * *
  ```

📌 Cron format is used

---

## 🔹 Build Environment (Optional)

Examples:

* Delete workspace before build
* Add timestamps to console output

✔ Recommended:

* **Add timestamps to the Console Output**

---

## 🔹 Build Section (MOST IMPORTANT)

Click:
👉 **Add build step**

### Common Build Steps:

#### Option 1: Execute Shell (Linux)

```bash
mvn clean install
```

Or

```bash
echo "Build started"
```

#### Option 2: Execute Windows Batch Command

```bat
mvn clean install
```

📌 This step compiles, tests, and builds the application

---

## 🔹 Post-build Actions

Used after build completion

### Common Options:

✔ **Archive the artifacts**

```text
target/*.jar
```

✔ **Email Notification**

* Send build status mail

✔ **Build other projects**

* Trigger downstream jobs

📌 Used in real-time CI/CD pipelines

---

## 7️⃣ Save the Job

👉 Click **Save** button

Your Jenkins Freestyle Job is now created 🎉

---

## 8️⃣ Run the Job

1. Open the Job
2. Click:
   👉 **Build Now**
3. Check **Console Output**

✔ Build Success → Job configured correctly
❌ Build Failure → Check logs

---

## 9️⃣ Important Interview Notes

* Jenkins Job is also called **Project**
* Freestyle job is UI-based
* Pipeline job uses **Jenkinsfile**
* Console Output is used for debugging
* Build triggers automate job execution

---

## 🔟 Summary

| Step | Action           |
| ---- | ---------------- |
| 1    | Open Jenkins     |
| 2    | Click New Item   |
| 3    | Enter Job Name   |
| 4    | Select Freestyle |
| 5    | Configure Job    |
| 6    | Add Build Steps  |
| 7    | Save & Build     |

---

✅ **You are now ready to work with Jenkins Freestyle Jobs**

---

> 📌 Next Topics (Optional):
>
> * Jenkins Pipeline Job
> * Jenkinsfile
> * CI/CD with Spring Boot
> * Jenkins + Git + Maven integration

Let me know what you want next 🙂
