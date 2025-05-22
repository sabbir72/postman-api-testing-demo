ঠিক আছে! আমি আপনার GitHub রিপো **`https://github.com/sabbir72/postman-api-testing-demo.git`** এর জন্য একটি সুন্দর এবং সম্পূর্ণ README ফাইল তৈরি করে দিলাম।

আপনি নিচের README.md কনটেন্টটি আপনার রিপোর মূল ডিরেক্টরিতে `README.md` নামে ফাইল বানিয়ে পেস্ট করতে পারেন:

```markdown
# Postman API Testing Demo

এই প্রজেক্টটি Postman এর API টেস্টগুলোকে GitHub Actions দিয়ে স্বয়ংক্রিয়ভাবে চালানোর জন্য তৈরি করা হয়েছে। এখানে আমরা Newman ব্যবহার করে টেস্ট চালাবো এবং HTML ফরম্যাটে রিপোর্ট তৈরি করব।

---

## 📂 প্রজেক্ট স্ট্রাকচার

```

.
├── postman\_collection.json
├── postman\_environment.json
├── .github/
│   └── workflows/
│       └── postman\_tests.yml

````

---

## 🚀 কিভাবে কাজ করে?

- যখনই `main` ব্রাঞ্চে কোড পুশ করবেন, GitHub Actions নিচের কাজগুলো করবে:
  1. আপনার কোড চেকআউট করবে
  2. Node.js সেটআপ করবে (ভার্সন 18)
  3. Newman ও Newman HTML রিপোর্টার ইনস্টল করবে
  4. Postman কলোকশন রান করবে নির্দিষ্ট environment ফাইলের সাহায্যে
  5. টেস্ট রিপোর্ট `reports/report.html` হিসেবে এক্সপোর্ট করবে
  6. রিপোর্ট ফাইলগুলো GitHub Artifacts হিসেবে আপলোড করবে

---

## 🛠️ GitHub Actions Workflow: `.github/workflows/postman_tests.yml`

```yaml
name: Run Postman Tests

on:
  push:
    branches: [ main ]

jobs:
  postman-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install Newman and HTML Reporter
        run: |
          npm install -g newman
          npm install -g newman-reporter-html

      - name: Create reports directory
        run: mkdir -p reports

      - name: Run Postman Tests
        run: |
          newman run postman_collection.json \
            --environment postman_environment.json \
            --reporters cli,html \
            --reporter-html-export reports/report.html

      - name: Upload report artifact
        uses: actions/upload-artifact@v4
        with:
          name: postman-report
          path: reports/
````

---

## 📋 লোকালি টেস্ট রান করা

আপনি চাইলে নিজের কম্পিউটারে Newman দিয়ে টেস্ট রান করতে পারেন:

```bash
npm install -g newman newman-reporter-html

newman run postman_collection.json \
  --environment postman_environment.json \
  --reporters cli,html \
  --reporter-html-export report.html
```

---

## 📂 রিপোর্ট কোথায় পাবেন?

* GitHub Actions এর রান শেষ হলে,
* রিপোতে যান → **Actions** ট্যাবে ক্লিক করুন
* সর্বশেষ রান ওপেন করুন
* নিচে **Artifacts** সেকশনে ক্লিক করে `postman-report` ডাউনলোড করুন
* ZIP আনজিপ করুন, তার ভিতরে পাবেন `report.html`
* ব্রাউজারে খুলে বিস্তারিত টেস্ট রিপোর্ট দেখুন

---

## 💡 গুরুত্বপূর্ণ নোটস

* `postman_collection.json` এবং `postman_environment.json` ফাইলগুলো রিপোর রুটে থাকা উচিত
* যদি অন্য ব্রাঞ্চে কাজ করেন, তাহলে `.yml` ফাইলের `branches` সেটিং পরিবর্তন করুন
* Ubuntu রানার ব্যবহার করা হয়েছে, Windows হলে স্ল্যাশ (`\`) এবং কমান্ড সিনট্যাক্স একটু ভিন্ন হবে

---

## 👤 লেখক

* Sabbir Ahmed ([@sabbir72](https://github.com/sabbir72))

---

---

**ধন্যবাদ!**
যদি সাহায্যের প্রয়োজন হয়, আমাকে জানাতে পারেন।

```

