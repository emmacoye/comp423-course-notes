# Setting up a dev container for Rust

* Primary author: [Emma Coye](https://github.com/emmacoye)
* Reviewer: [Manasi Chaudhary](https://github.com/mchaudh-21)

## Prerequisites

Before you begin this process you should install the following:

* Visual Studio Code
* Docker Desktop
* Dev Containers (Visual Studio Code Extension) --> this will automatically install the extension for Rust Analyzer

You should also have a general understanding of:

* Github 
* Git

## Create Your New Project

### 1. Initialize Git Repository 

Open your terminal or a command line prompt and type the following lines of code:

``` bash
# Create and enter new directory 
mkdir rust-hello-423 
cd rust-hello-423

# Initialize git repository 
git init 

# Create initial commit with an empty README file
echo "# Rust Hello COMP423" > README.md
git add README.md
git commit -m "Initial Commit For New Project"
```
!!! note 
    Initializing a git repository will allow you to track your changes and collaborate with teammates easily if necessary.

#### Create a Remote Repository on GitHub
(1) Log in to your GitHub account and navigate to the Create a New Repository page.

(2) Fill in the details as follows:

- Repository Name: rust-hello-comp423
- Description: Something releated to how this is a "Hello World" program.
- Visibility: Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click Create Repository.

#### Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote:


``` bash
git remote add origin https://github.com/<your-username>/rust-hello-comp423.git
```
- Replace <your-username> with your GitHub username.

(2) Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: git branch -M main. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

(3) Push your local commits to the GitHub repository:


``` bash
git push --set-upstream origin main
```

!!! Understanding the --set-upstream Flag
    git push --set-upstream origin main: This command pushes the main branch to the remote repository origin. The --set-upstream flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing git push origin when working on your local main branch. This long flag has a corresponding -u short flag.
(4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

!!! Reference
    These instructions are from COMP 423's [mkdocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-3-link-your-local-repository-to-github).



### 2. Configure a Dev Container 

Open Visual Studio Code and navigate to your newly created directory.
In the root of your project, create a new ```.devcontainer``` directory and add a ```devcontainer.json``` file. 
This will be considered "hidden". 

Add the following configuration within this file:
```
{
    "name": "Rust",
    "image": "mcr.microsoft.com/devcontainers/rust:1-bullseye",
    "customizations":{
        "vscode":{
            "settings": {},
            "extensions": ["rust-lang.rust-analyzer"]
        }
    },
    "postCreateCommand": "",
    "remoteUser": "vscode"
}
```

After adding the above configurations, we then want to reopen our project in a dev container.
To do so press Ctrl+Shift+P (or Cmd+Shift+P on macOS) and type: 
"Dev Containers: Reopen in Container," and selecting the option.

### 3. Create Your Rust Project
Inside the container, let's verify that Rust is installed and is up-to-date with its version.
In VS Code, write the following in the terminal:

``` bash
rustc --version
```

Now use the cargo new command to create a binary project
``` bash
cargo new hello_comp423 --vcs none
```

!!! Note
    Use the flag that does not create a new git repository automatically on your behalf: --vcs none (Version Control System).

Then, navigate to this new project by typing:

``` bash
cd hello_comp423
```

### 4. Let's Code The "Hello COMP423" Program
In your project src folder, find the file called ```main.rs``` and write the following code in the file:

```
fn main() {
    println!("Hello COMP423");
}
```

### 5. Build and Run Your New program
We can compile and run the program in two different way (your directory should be ```/workspaces/rust-hello-comp423/hello_comp423```):

- ### Use ```cargo build```

In your terminal write the following command to compile your program
``` bash
cargo build
```
Then, you can see your executable file under the ```target/debug``` directory.
In your terminal, you can then write the following code to run your program:
``` bash
./target/debug/hello_comp423
```
!!! note
    This is a very similar process to using the ```gcc ``` commands that you have used in COMP 211.

- ### Use ```cargo run```

To compile and run in one step, you can write the following code in your terminal:

```bash
cargo run
```

This should output ```Hello COMP423```.

### 6. Push Changes and Deploy
Now that your program runs successfully, let's add and commit the changes to your remote repository. 
```
    # Add and commit changes
    git add .
    git commit -m "Created Hello COMP423 in Rust"

    # Push changes to remote repo 
    git push origin main
```
Check that the changes have been committed and pushed to your remote repo on GitHub. 

## Congrats! 
You've written ```Hello COMP423``` in Rust.

## References

Details on dev containers and mkdocs can be further explored with this COMP 423 [mkdocs tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#what-is-a-development-dev-container).