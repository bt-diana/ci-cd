# CI/CD, Accessibility & Performance Optimization Project

This project is a completed task from [The RS School](https://rs.school/) ShortTrack course aimed at practicing real-world development workflows and quality improvements.

The goal of the task was to:
- Set up a complete **CI/CD pipeline** using GitHub Actions
- Implement **accessibility improvements** based on Lighthouse reports
- Perform **performance optimization** using DevTools and modern web practices

🚀 Deployment: [before](https://joyful-puppy-de9da6.netlify.app/) | [after](https://feature-ci-cd--joyful-puppy-de9da6.netlify.app/)


## Features

### 🔄 CI/CD Setup

The project includes a fully functional CI/CD pipeline configured with **GitHub Actions** and **Netlify**.  
The goal was to automate quality checks for every commit and ensure safe and smooth deployment.

#### 🔐 Branch Protection
To prevent direct pushes to `main`, a **branch protection rule** was added:

- "Require a pull request before merging" is enabled.
- "Require status checks to pass before merging" ensures that builds and tests must pass.

![Branch protection rule](https://github.com/user-attachments/assets/9d8f6b38-38e1-4322-8724-e7b2e60995b8)  
![Require status checks](https://github.com/user-attachments/assets/ed9ac0f2-8557-4688-94e8-fb4415f9ffce)  
![Checks blocked merge](https://github.com/user-attachments/assets/7ca2b0d7-503c-4f7a-91a3-2ddfcaf1cf81)

#### ✅ Commit Validation Workflow

A GitHub Actions workflow [`commit-validation.yml`](https://github.com/bt-diana/ci-cd/blob/feature/ci-cd/.github/workflows/commit-validation.yml) was created to validate every commit pushed to any `feature/*` branch.  
The workflow performs the following steps:

- Checkout the repository
- Install Node.js
- Install dependencies from `package-lock.json`
- Run `npm run lint`
- Run `npm run test`
- Run `npm run build`

This ensures all commits follow code quality standards and are buildable.

#### 🚀 Pull Request Checks

When a pull request is opened or updated against `main`, the same validation workflow runs automatically.  
Thanks to the branch protection rules, **a PR cannot be merged unless all checks pass**.

#### 🏷️ Branch Name Validation

To enforce a consistent branching strategy, another workflow [`branch-naming.yml`](https://github.com/bt-diana/ci-cd/blob/feature/ci-cd/.github/workflows/branch-naming.yml) checks that all PR branches targeting `main` start with `feature/`.

#### 🌐 Deployment Pipeline

A deployment pipeline was configured in [`deployment.yml`](https://github.com/bt-diana/ci-cd/blob/feature/ci-cd/.github/workflows/deployment.yml) using the [Netlify Deploy GitHub Action](https://github.com/marketplace/actions/netlify-deploy).  
It automatically deploys preview builds of the app for **every push** to a branch that has an **open pull request**.

This allows reviewers to test the latest version of the app before merging into `main`.


### ♿ Accessibility Improvements
- Accessibility score increased to **≥95** in Lighthouse.
- **Contrast fixes**: unified and darkened color palette for better text readability.
- **Aria labels** added to key interactive elements:
  - Price and stock inputs
  - Sliders and thumbs
  - Search field
- **Touch targets** improved by increasing slider sizes and enabling pointer events.

**Before:**  
![Before Accessibility](https://github.com/user-attachments/assets/68a189da-df51-452a-9283-535cc3435efc)  

**After:**  
![After Accessibility](https://github.com/user-attachments/assets/c5cbd0c8-adf7-4da0-a7c3-441382fcf9d9)

### ⚡ Performance Optimization
- **Initial metrics** (FCP, LCP, CLS, Speed Index) documented via Lighthouse and DevTools.
- Optimizations implemented include:
  - Defined image sizes to avoid layout shifts
  - Converted all thumbnails to `.webp`
  - Added `loading="lazy"` to off-screen assets
  - Self-hosted fonts to reduce render-blocking
  - Resized and optimized hero image (`eucalypt`) for faster LCP

**Before:**  
![Lighthouse Before](https://github.com/user-attachments/assets/cf72864d-2b46-4701-9610-95f25bc1cb7b)  
![DevTools Before 1](https://github.com/user-attachments/assets/34c3c480-21bc-416d-8ad6-075b22104640)  
![DevTools Before 2](https://github.com/user-attachments/assets/fcc371ec-a060-4594-917e-457d79567a12)  

**After:**  
![Lighthouse After](https://github.com/user-attachments/assets/74b070ab-e12d-4616-8f78-48b0994678cf)  
![DevTools After](https://github.com/user-attachments/assets/e91abb21-3a7d-4cf0-b240-7ffd562d2687)


## Technologies Used

- **GitHub Actions** – for automating CI/CD workflows
- **Netlify Deploy Action** – for auto-deploying preview builds
- **Lighthouse + Chrome DevTools** – for measuring and improving performance & accessibility
