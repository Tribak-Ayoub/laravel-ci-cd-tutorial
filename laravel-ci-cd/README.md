## 🚀 Full Beginner Tutorial: CI/CD for Laravel App using GitHub Actions

---

### 📌 What you’ll do:

1. Create a new Laravel app
2. Set up Git and push to GitHub
3. Create a GitHub Actions workflow
4. Run tests (pass & fail) automatically on push (CI)
5. Simulate deployment if tests pass (CD)

---

## 📦 Step 1: Create a Laravel App

---

### ✅ Prerequisites

-   PHP >= 8.1
-   Composer
-   Git
-   Laravel installer (`composer global require laravel/installer`)
-   MySQL or SQLite (optional for testing)

---

### 🧱 Step 1.1: Create your Laravel project

```bash
laravel new laravel-ci-cd
cd laravel-ci-cd
```

Or using Composer:

```bash
composer create-project laravel/laravel laravel-ci-cd
cd laravel-ci-cd
```

Test it locally:

```bash
php artisan serve
```

---

### 🧪 Step 1.2: Run Laravel’s default test

```bash
php artisan test
```

You should see a green ✅ result.

---

## 🗃️ Step 2: Initialize Git and Push to GitHub

---

```bash
git init
git add .
git commit -m "Initial Laravel commit"
```

Create a repo on GitHub (e.g., `laravel-ci-cd`) and push:

```bash
git remote add origin https://github.com/YOUR_USERNAME/laravel-ci-cd.git
git branch -M main
git push -u origin main
```

---

## ⚙️ Step 3: Add GitHub Actions Workflow

---

### 🗂️ Step 3.1: Create Workflow Directory

```bash
mkdir -p .github/workflows
touch .github/workflows/ci-cd.yml
```

---

### 🛠️ Step 3.2: Add CI/CD Workflow to `ci-cd.yml`

```yaml
name: Laravel CI/CD

on:
    push:
        branches:
            - main

jobs:
    build:
        runs-on: ubuntu-latest

        steps:
            - name: Checkout code
              uses: actions/checkout@v2

            - name: Set up PHP
              uses: shivammathur/setup-php@v2
              with:
                  php-version: "8.2"
                  extensions: mbstring, bcmath, sqlite

            - name: Install Composer dependencies
              working-directory: ./laravel-ci-cd
              run: composer install --no-progress --prefer-dist

            - name: Copy .env file
              working-directory: ./laravel-ci-cd
              run: cp .env.example .env

            - name: Generate Laravel application key
              working-directory: ./laravel-ci-cd
              run: php artisan key:generate

            - name: Run Tests
              working-directory: ./laravel-ci-cd
              run: php artisan test

            - name: Simulate deployment
              run: echo "Deploying Laravel app..."
```

✅ This sets up PHP, installs Laravel dependencies, runs the default tests, and then simulates deployment.

---

## 🧪 Step 4: Test All Cases

---

### ✅ Case A: All tests pass

-   Push code to GitHub:
    ```bash
    git add .
    git commit -m "Test CI passing"
    git push
    ```
-   Go to GitHub → Actions tab → see the workflow run
-   You'll see ✅ all tests pass and deployment message

---

### ❌ Case B: Add a failing test

Edit or add a new test in `tests/Feature/ExampleTest.php`:

```php
public function test_failing_test(): void
{
    $this->assertTrue(false); // This will fail
}
```

Push the change:

```bash
git add .
git commit -m "Add failing test"
git push
```

-   Go to GitHub → Actions tab
-   ❌ You’ll see the workflow fails on `Run tests`, and **deployment won’t run**

---

### ✅ Case C: Fix the test and push again

```php
public function test_failing_test(): void
{
    $this->assertTrue(true); // Now it will pass
}
```

Then push:

```bash
git commit -am "Fix test"
git push
```

✅ You’ll see a full successful CI/CD pipeline.

---

## 🎉 Bonus: Laravel-Specific Tips

-   Use `.env.testing` to configure test DB (e.g., SQLite)
-   Add PHPStan, Pint, or PHPUnit reports to your workflow
-   You can SSH and deploy to a real server later using `scp` or `rsync`
