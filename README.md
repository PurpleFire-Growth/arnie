
# Shopify Theme Development Workflow

## Local Development:

#### Install Global Dependencies:
```bash
npm install -g @shopify/cli @shopify/theme
```

#### Clone the Repository:
```bash
git clone https://github.com/PurpleFire-Growth/arnie.git
```

#### Ensure Ruby is installed:
Follow the [Ruby installation guide](https://www.ruby-lang.org/en/documentation/installation/).

#### Create `shopify.theme.toml` File:
```bash
[environments.development]
store = "https://arniesgar.myshopify.com/"
```

#### Start Development Server:
```bash
shopify theme dev -e development
```

---

## Git Branching Workflow

We use three main types of branches:

- `master`: Represents the live (production) store.
- `pre-deploy`: A staging branch for final checks before merging into `master`.
- Feature branches: Named as `feature/xyz`, for individual tasks or features. These branches follow naming conventions but do not necessarily refer to a "feature" type of task.

### Creating Branches:

#### 1. **Master Branch:**
This branch represents the **live store**. Only thoroughly tested and approved changes should be merged into this branch.
```bash
git checkout master
```

#### 2. **Pre-Deploy Branch:**
This branch is used as a **staging environment**. All features or fixes should be merged here for final testing before going to production. **It is crucial that `pre-deploy` is always kept up to date with the latest changes from `master` before creating pull requests.**
```bash
git checkout pre-deploy
git pull origin master
```

#### 3. **Feature Branches:**
These branches are created from `master`. They are named following the convention `feature/xyz` but can be used for any type of task, including bug fixes, documentation, refactors, etc.
```bash
git checkout -b feature/ABC-123/short-description
```

---

## Production Deployment:

#### Create a Branch for Your Changes:
Always create a branch from `master`, regardless of the type of task (feature, bugfix, etc.).
```bash
git checkout -b feature/ABC-123/add-new-feature
```

#### Make Changes and Commit:
Make the necessary changes, then commit following the commit-lint format:
```bash
git add .
git commit -m "feat: Add new feature

This feature allows users to do something new.

ABC-123"
```

#### Create a Pull Request:
Push your feature branch and create a pull request against the `pre-deploy` branch. **Ensure that `pre-deploy` is fully updated with the latest changes from `master` before merging your feature branch.**
```bash
git checkout pre-deploy
git pull origin master
```

Once your changes are reviewed and approved, they will be merged into `pre-deploy`.

Notify the team in Slack when your pull request is ready.

#### Merging to Master:
After successful testing on the `pre-deploy` branch, `pre-deploy` can be merged into `master`.

---

<details>
<summary>Example Workflow:</summary>

1. **Create a Feature Branch from Master:**
```bash
git checkout -b feature/ABC-123/add-product-carousel
```

2. **Make Your Changes:**

Edit the code, then commit using the following format:
```bash
git add .
git commit -m "feat: Add product carousel

Implemented a new product carousel on the homepage to enhance the user experience.

ABC-123"
```

3. **Push the Feature Branch:**
```bash
git push origin feature/ABC-123/add-product-carousel
```

4. **Create a Pull Request:**
Ensure `pre-deploy` is up to date with `master`:
```bash
git checkout pre-deploy
git pull origin master
```

Then create a pull request to merge `feature/ABC-123/add-product-carousel` into `pre-deploy`. After review and approval, it will be merged into `pre-deploy`.

5. **Merge into Master:**
Once testing is complete on the `pre-deploy` branch, create a pull request to merge `pre-deploy` into `master`.

</details>

---

<details>
<summary>Task Abbreviations:</summary>

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Non-functional changes (formatting, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or correcting tests
- `chore`: Updates to build processes or auxiliary tools

</details>

---

With this structure, you ensure that `pre-deploy` is always synchronized with `master`, preventing any discrepancies during the staging process. This keeps the workflow stable and consistent for deployment.