# Setting up a Dev Container for Rust

* Primary author: [Shayna Patel](https://github.com/shaynapat3l)

* Reviewer: [Bhavika Lingutla](https://github.com/bhavikal)

This tutorial will guide you through setting up a Rust development environment using Dev Containers. By the end of the tutorial, you will have a working Rust project that prints *'"Hello COMP423"'* to standard output.

!!!info
    Some snippets of this tutorial were taken from or inspired by Kris Jordan's [COMP 423 MkDocs Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-create-a-remote-repository-on-github").
    
## Prerequisites :heart:

Before you begin, make sure you have the following installed and set up:

1. **A GitHub account**: If you don't have one yet, sign up at [GitHub](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
2. **Git Installed**: Install Git from [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
3. **Docker installed**: Required to run the Dev Container. Get [Docker](https://www.docker.com/products/docker-desktop/).
4. **Visual Studio Code (VS Code)**: Download and install it from [here](https://code.visualstudio.com/).
5. **Command-line basics**: You can review this [resource](https://www.w3schools.com/whatis/whatis_cli.asp).


## Step 1: Create a New Dev Container Project :face_with_monocle:

**(A)** Open your terminal and create a directory for your project:
```bash
mkdir comp423-rust-dev
cd comp423-rust-dev
```

**(B)** Initialize a new Git repository:
```
git init
```

**(C)** Create a README.md file:
```
echo "# Rust Dev Container Project" > README.md
echo "To view the entire tutorial, visit https://shaynapat3l.github.io/comp423-course-notes/" >> README.md
git add README.md
git commit -m "Initial commit with README"
```

!!!tip 
    Initializing Git and adding a README ensures your project is ready for version control and collaboration.


## Step 2: Create a Remote Repository on GitHub :alien_monster:

**(A)** Log in to your GitHub account and navigate to the *Create a New Repository* page.

**(B)** Fill in the details as follows:

+ ***Repository Name***: `comp423-rust-dev`
+ ***Description***: "A Rust project using Dev Containers"
+ ***Visibility***: Public
+ Do not initialize the repository with a README, `.gitignore`, or license.
+ Click ***Create Repository***.


## Step 3: Link Your Local Repository on GitHub :link:

**(A)** Add the GitHub repository as a remote:
```
git remote add origin https://github.com/<your-username>/comp423-rust-dev.git
```

!!!warning
    Replace `<your-username>` with your GitHub username.

**(B)** Check your default branch name with the following command (it should be `main`):
```
git branch
```

!!!note
    If the default branch is not `main`, rename it using `git branch -M main`.


**(C)** Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```

**(D)** Refresh your GitHub repository in your web browser to confirm that your local commits have been pushed to the remote repository.


## Step 4: Configure the Dev Container :gear:

**(A)** Open the `comp423-rust-dev` directory in Visual Studio Code by going to: File > Open Folder.

!!!note
    Make sure to install the Dev Containers extension for VS Code.


**(B)** Create a `.devcontainer` directory in the project root:
```
mkdir .devcontainer
```

**(C)** Inside `.devcontainer`, create a `devcontainer.json` file.

+ The `.devcontainer.json` file defines the configuration for your development environment. It specifies:
    + `name`: A descriptive name for your dev container.
    + `image`: The Docker image to use, in this case, the latest version of a Rust environment.
    + `customizations`: Adds useful configurations to VS Code.


**(D)** Add the following content to `devcontainer.json`:
```
{
    "name": "Rust Dev Environment",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "rust-lang.rust-analyzer"
            ]
        }
    }
}
```

!!!note
    This configuration uses Microsoft's offical Rust image and installs the `rust-analyzer` extension automatically.


**(E)** Reopen the folder in a Dev Container.

- Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS) and select *Remote-Containers: Reopen in Container*.

!!!warning
    If the container fails to build, verify your Docker installation and ensure the `devcontainer.json` file is correctly configured.


## Step 5: Verify Rust Installation :check_mark:

**(A)** Inside the Dev Container, check the Rust version by typing the following in your terminal:
```
rustc --version
```

!!!warning
    If the version is outdated, run `rustup update` to ensure you have the latest version of Rust. As of January 2025, the latest version of Rust is 1.84.0, released on January 9, 2025.


## Step 6: Create a Rust Project :woman_technologist:

**(A)** Use the `cargo new` command to create a new binary project:
```
cargo new hello-comp423 --vcs none
cd hello-comp423
```

!!!note
    The `--vcs none` flag ensures that Cargo does not create a Git repository automatically.


## Step 7: Write the program :pencil:

**(A)** Open the `src/main.rs` file and modify it to print *"Hello COMP423"*:
```
fn main() {
    println!("Hello COMP423");
}
```


## Step 8: Compile and Run the Program :card_index_dividers:

**(A)** Use `cargo build`:

1. In your terminal, compile the project:
    ```
    cargo build
    ```
2. Run the compiled binary manually:
    ```
    ./target/debug/hello-comp423
    ```
    + Example Output:
    ```
    Hello COMP423
    ```

!!!tip
    `cargo build` is similar to gcc in COMP211. It compiles your source code into an executable file.

**(B)** Alternatively, you can use `cargo run`:

1. Use the `cargo run` command to compile and execute the program in one step:
    ```
    cargo run
    ```

!!!note
    While `cargo build` compiles the project and generates an excutable file whicn then must be manually run, `cargo run` combines the build and execution steps into a single command.


## Step 9: Push Changes and Deploy :star_struck:

**(A)** Add and commit your changes:
    ```
    git add .
    git commit -m "Rust tutorial with Dev Container"
    ```

**(B)** Push your changes to Github:
    ```
    git push origin main
    ```
