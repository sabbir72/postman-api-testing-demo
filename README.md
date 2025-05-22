

````markdown
# 🚀 Postman CI/CD Automation

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/your-username/postman-ci-cd/postman_tests.yml?branch=main&label=CI%2FCD)](https://github.com/your-username/postman-ci-cd/actions/workflows/postman_tests.yml)

Automate your API testing seamlessly with **Postman** and **GitHub Actions**!  
This project demonstrates how to run Postman API tests automatically on every push to your repository using **Newman**, generate beautiful HTML reports, and store them as build artifacts — all powered by Continuous Integration and Delivery (CI/CD).

---

## 🎯 Why Use This?

- **Automated API Testing:** Ensure your APIs work correctly after every code change  
- **CI/CD Integration:** Run tests automatically via GitHub Actions without manual intervention  
- **Clear Reports:** Generate easy-to-read HTML reports for test results  
- **Version Control:** Keep your test collections and environments under Git version control  
- **Open Source Ready:** Customize and extend for your own projects effortlessly  

---

## 📦 Project Structure

```plaintext
postman-ci-cd/
├── postman_collection.json          # Your Postman API test collection
├── postman_environment.json         # Environment variables for your tests
├── .github/
│   └── workflows/
│       └── postman_tests.yml        # GitHub Actions workflow to run Newman tests
├── README.md                        # This file (project documentation)
````

---

## 🔧 How It Works

* **Trigger:** When you push code to the `main` branch, GitHub Actions triggers the workflow
* **Setup:** Installs Node.js, Newman CLI, and HTML reporter globally
* **Run Tests:** Executes the Postman collection using Newman with environment variables
* **Report:** Generates an HTML report and stores it inside the `reports` folder
* **Upload:** Uploads the report as a GitHub Actions artifact for easy download and review

---

## ⚡ Quick Start

### Run Tests Locally

If you want to test your collection on your local machine:

```bash
npm install -g newman newman-reporter-html

newman run postman_collection.json \
  --environment postman_environment.json \
  --reporters cli,html \
  --reporter-html-export report.html
```

Open `report.html` in your browser to see the test results.

---

### View GitHub Actions Report

1. After pushing code, go to your GitHub repository
2. Click on the **Actions** tab
3. Select the latest **Run Postman Tests** workflow
4. Scroll down to **Artifacts**, download the `postman-report.zip`
5. Extract and open `report.html` to review test outcomes

---

## 📋 GitHub Actions Workflow (`.github/workflows/postman_tests.yml`)

```yaml
name: Run Postman Tests

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install Newman & HTML Reporter
        run: |
          npm install -g newman newman-reporter-html

      - name: Create reports folder
        run: mkdir -p reports

      - name: Run Postman Collection
        run: |
          newman run postman_collection.json \
            --environment postman_environment.json \
            --reporters cli,html \
            --reporter-html-export reports/report.html

      - name: Upload Report Artifact
        uses: actions/upload-artifact@v4
        with:
          name: postman-report
          path: reports/
```

---

## 🙌 Contribution

Feel free to fork this repo, open issues, and submit pull requests.
Your feedback and contributions are always welcome!

---


---

## 👤 Author

**Sabbir Ahmed**
[GitHub: @sabbir72](https://github.com/sabbir72)
Email: [sabbir72@example.com](mailto:sabbircse72@gmail.com)

---

