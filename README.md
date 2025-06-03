
# 🚀 Laravel CI/CD Pipeline with GitHub Actions

This repository demonstrates a simple **CI/CD pipeline** for a Laravel application using **GitHub Actions**.

---

## 📦 About

This Laravel project runs **automated tests** on every push to the `main` branch (CI), and **simulates deployment** if tests pass (CD). The pipeline is configured using a GitHub Actions workflow.

---

## 🧰 Tech Stack

- Laravel 11+
- PHP 8.2
- Composer
- GitHub Actions
- SQLite (for testing)

---

## ⚙️ CI/CD Workflow

Located in: `.github/workflows/ci-cd.yml`

### 🧪 Continuous Integration (CI)
On each push to `main`:
- Installs dependencies
- Generates app key
- Runs tests with `php artisan test`

### 🚀 Continuous Deployment (CD)
- Only runs if tests pass
- Simulates deployment using `echo` (can be replaced with real deployment steps)

---

## 🚀 Getting Started Locally

```bash
# Clone repo
git clone https://github.com/YOUR_USERNAME/laravel-ci-cd.git
cd laravel-ci-cd

# Install dependencies
composer install

# Copy environment file
cp .env.example .env

# Generate application key
php artisan key:generate

# Serve the app
php artisan serve
```

---

## 🧪 Running Tests

```bash
php artisan test
```

> Uses the default Laravel tests in `tests/Feature`.

---

## 🔁 Testing the Pipeline

### ✅ All Tests Pass
- Push to `main`
- GitHub Actions runs CI/CD and prints:
  ```
  Deploying Laravel app to production...
  ```

### ❌ Tests Fail
- Add a failing test (e.g. `assertTrue(false)`)
- Push to `main`
- Pipeline stops at test step and **does not deploy**

---

## 📂 Project Structure (partial)

```
laravel-ci-cd/
├── app/
├── tests/
│   └── Feature/
│       └── ExampleTest.php
├── .github/
│   └── workflows/
│       └── ci-cd.yml
├── artisan
├── composer.json
└── README.md
```

---

## 📸 GitHub Actions Preview

| CI Step         | Status |
|----------------|--------|
| Checkout code  | ✅     |
| Setup PHP      | ✅     |
| Install Deps   | ✅     |
| Run Tests      | ✅/❌  |
| Deploy (echo)  | ✅/—   |

---

## ✅ Future Improvements

- Add real deployment to VPS or Laravel Forge
- Integrate code style checks (Laravel Pint)
- Add static analysis tools (PHPStan)
- Use MySQL/PostgreSQL for more realistic test environments

---

## 🤝 License

Open-source project under the [MIT License](LICENSE).
