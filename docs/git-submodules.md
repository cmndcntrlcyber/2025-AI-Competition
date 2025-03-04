# Git Submodules

## Description

Using **Git submodules** is another excellent approach to combine two Git repositories, especially when you want to keep each repository independent but still have them linked in a parent project. Submodules allow you to embed one Git repository within another and treat it as a separate entity while keeping the repositories' histories intact.

Here’s how you can use submodules to combine two repositories:

### 1. **Choose Which Repo Will Be the Parent**

   Decide which repository will be the "parent" or "main" repository that will contain the submodule.

### 2. **Navigate to the Parent Repository**

   In your terminal, navigate to the main repository (the one that will host the submodule).

   ```bash
   cd /path/to/parent-repo
   ```

### 3. **Add the Second Repository as a Submodule**

   Add the second repository as a submodule inside the parent repository. You can specify a directory where you want the submodule to be placed.

   ```bash
   git submodule add <url-of-second-repo> <path-to-submodule-directory>
   ```

   For example:

   ```bash
   git submodule add https://github.com/username/second-repo.git submodule-folder
   ```

   This will:

- Clone the second repository into the specified directory (`submodule-folder`).
- Add an entry in the `.gitmodules` file that tracks the submodule configuration.

### 4. **Commit the Submodule Changes**

   Git will automatically add changes to the parent repository, including a new `.gitmodules` file and a reference to the commit of the submodule.

   You need to commit these changes:

   ```bash
   git add .gitmodules submodule-folder
   git commit -m "Added second repo as a submodule"
   git push origin main
   ```

### 5. **Working with Submodules**

   Now that the second repository is added as a submodule, you can interact with it in a few ways:

- **To initialize submodules (if cloning the parent repo):**

     If someone else clones the parent repository or you are working in a new environment, they need to initialize the submodule:

     ```bash
     git submodule init
     git submodule update
     ```

- **To update the submodule to the latest commit:**

     If the submodule repository gets updated and you want to pull the latest changes, you can do:

     ```bash
     git submodule update --remote
     ```

- **To go into the submodule directory and work:**

     You can navigate into the submodule directory and treat it like a normal Git repository. For example:

     ```bash
     cd submodule-folder
     git checkout <branch>
     git pull origin <branch>
     ```

### 6. **Commit Changes in the Submodule**

   If you make changes inside the submodule (e.g., by updating the submodule to a new commit or making edits directly within the submodule), you'll need to commit those changes in both the submodule and the parent repository.

- **In the submodule:**

     ```bash
     cd submodule-folder
     git add .
     git commit -m "Changes in submodule"
     git push origin main
     ```

- **In the parent repository:**
     After updating the submodule, you need to commit the change in the parent repository, which tracks the submodule’s commit.

     ```bash
     cd /path/to/parent-repo
     git add submodule-folder
     git commit -m "Updated submodule to latest commit"
     git push origin main
     ```

### 7. **Remove a Submodule (If Needed)**

   If you decide that you no longer want the submodule, you can remove it:

   ```bash
   git submodule deinit submodule-folder
   git rm submodule-folder
   git commit -m "Removed submodule"
   git push origin main
   ```

   This will remove the submodule from your parent repository and the `.gitmodules` file.

---

### When to Use Submodules

Using submodules is especially useful when:

- You want to include a third-party repository or another project as part of your project but keep them separate.
- You need to maintain multiple Git repositories with distinct histories while keeping them linked together.
- You have one large project that consists of multiple smaller projects that each need their own versioning.

### Things to Keep in Mind

- **Submodules are separate repositories:** While they are integrated into the parent repository, they still function independently. You need to manage them separately (e.g., cloning, pulling updates).
- **Tracking submodule commits:** The parent repository only tracks the commit of the submodule. If you want to get updates from the submodule, you must manually update it.
- **Complexity:** Submodules can introduce some complexity when it comes to managing changes and syncing them between repositories. It’s important to understand the workflow for pushing changes to both the submodule and the parent repository.

### Summary

Using Git submodules is a great way to combine two repositories if you need to keep them distinct but still reference one repository inside the other. The main benefit of submodules is that each repository keeps its own history, while you can control and update their versions within the parent project.
