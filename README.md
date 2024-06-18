# Visual Studio Code for the Bedford Lab

*Victor Lin, 18 June 2024*

A guide on practical uses for the popular text editor by members of the Bedford
Lab.

The first few sections were written for an interactive follow-along demo during
lab meeting, but overall this was written with the intent to be referenced
outside of the demo.


## Getting started

1. [Download] Visual Studio Code (VS Code)
2. Use this template repository to create your own repository
3. Clone your repository using [git]
4. Open the repository folder in Visual Studio Code. Two methods:
    1. Select File > **Open Folder**
    2. Navigate to the folder in a terminal and run `code .`

> [!NOTE]
> You can also open a specific file with `code path/to/file`, but most other
> features in this guide rely on opening a folder in VS Code.

[Download]: https://code.visualstudio.com/download
[git]: https://www.git-scm.com


## What's on my screen?

- Editor area
    - Tab Bar
- Side Bar
    - Activity Bar
- Top bar  <!-- I made up this name - it's really a combination of Command Center, Layout Controls, and Editor Actions -->
- Status Bar

Learn more: [Visual Studio Code User Interface](https://code.visualstudio.com/docs/getstarted/userinterface)

<!-- DEMO

- show sticky scroll
- show breadcrumbs
- show file outline in Explorer
- show markdown preview (noting that the editor can show non-editable stuff)

-->


## What's not on my screen?

- Command pallette
- Panel


## Command Palette

The Command Palette allows you to:

- Run commands (`>`)
- Go to symbols (`@`, `#`)
- Open files (no prefix)
- Search for more functionality (`?`)

You can activate it by clicking the search area in the top bar or using a
keyboard shortcut.

> [!TIP]
> Clicking around lets you explore features. As you get comfortable with VS
> Code, you may find it easier to use keyboard shortcuts to do common tasks.

Learn more: [Visual Studio Code User Interface: Command Palette](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette)


## Terminal

The terminal opens a shell using the root folder as your current working
directory.

Open the terminal using the command `View: Toggle Terminal`.

Learn more: [Integrated Terminal in Visual Studio Code](https://code.visualstudio.com/docs/terminal/basics)

<!-- DEMO

- run git status

-->


## Source Control

Source Control is the branching icon in the Activity Bar. It provides a visual
way to interact with `git`.

Try making a commit and pushing it:

1. Go to the Explorer and create a new file
2. Go to Source Control and stage the new file (＋)
3. Type a commit message and commit it (✔️)
4. Push the commit to GitHub (sync changes)

> [!TIP]
> If you prefer to use `git` through another terminal app, you can still use VS
> Code for things such as editing commit messages, viewing diffs, and resolving
> merge conflicts: [VS Code as Git editor]

Learn more: [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview)

[VS Code as Git editor]: https://code.visualstudio.com/docs/sourcecontrol/overview#_vs-code-as-git-editor

<!-- DEMO

- walk through the steps above
- view a diff
- show the 3-way merge editor
    example: nextstrain.org merging 096c3fe34705411e4a57acb8cc1537a3116cc538 into e70f5304ce0969d9e0214a043d9c3438df91ee2c

-->


## Working from a remote SSH host (e.g. `rhino`)

Sometimes you may want to do work on a remote server. The normal process would
be to open a terminal, connect using `ssh`, and do stuff within the terminal.

Instead of interacting with the server through a text-based terminal, you can
connect to it using VS Code and take advantage of all the features that have
been described.

These steps describe how to connect VS Code to the `rhino` Hutch cluster.

1. Install the [Remote - SSH] extension
2. Open the Command Palette
3. Search for and run the command **Remote-SSH: Connect to Host...**
4. If you see an entry for `rhino`, select it. You may have to enter a password
   (but there are [ways around that]!)
5. If you do not see an entry for `rhino`, you will need to set it up:
    1. Select **Add New SSH Host...**
    2. Enter `ssh user@rhino` for the SSH command, replacing `user` with your
       HutchNet ID
    3. Select an SSH configuration file to update (if unsure, pick the first one)
6. Ignore the warnings about `rhino` being unsupported (it's just running an
   older version of Linux)
7. Go to the **Explorer** view
8. Open a folder
9. Do stuff!

> [!TIP]
> You can use the Explorer to upload/download files.

[Remote - SSH]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh
[ways around that]: https://code.visualstudio.com/docs/remote/troubleshooting#_configuring-key-based-authentication

<!-- rhino wiki page if needed: https://sciwiki.fredhutch.org/compdemos/howtoRhino/ -->


## Working from a Docker image (e.g. `nextstrain/base`)

Sometimes you may want to do work within a Docker container. The normal process
would be to open a terminal, run `docker run -it` or a wrapper around that such
as `nextstrain shell`, and do stuff within the terminal.

Similar to the SSH scenario, you can use VS Code in this situation.

These steps describe how to use VS Code to start and connect to a container
based on the Nextstrain Docker image.

1. Create a file `.devcontainer.json` in your root folder with these contents:

    ```json
    {
        "image": "nextstrain/base:build-20240617T235011Z"
    }
    ```

2. Go to the **Remote Explorer** view
3. Select **reopen the current folder in a container** (this may take a while to
   pull the image file)

> [!TIP]
> `.devcontainer.json` is a file used for your VS Code setup. It's likely that
> you want to keep this file out of source control across projects. This can be
> done by configuring a [global gitignore file].

[global gitignore file]: https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#_core_excludesfile


## Working from a GitHub codespace

[GitHub codespaces] are remote Docker containers run on GitHub-hosted VMs. I use
them occasionally when I want to test something on a fresh environment (e.g.
Nextstrain installation). It's easy to start a codespace and connect using VS
Code.

[GitHub codespaces]: https://docs.github.com/en/codespaces/overview


## Text editors vs. integrated development environments (IDEs)

You may be familiar with some IDEs, which can be thought of as text editors
optimized for a specific programming language with extended capabilities for
debugging, code completion, and other things.

- RStudio
- PyCharm
- IntelliJ
- Eclipse

VS Code comes out of the box as a text editor, but extensions can be installed
which enable functionalities that are characteristic of IDEs.

## Running Python code

The [Python extension] comes with a debugger to allow interactive inspection of
variables when running a script.

There is also a [Jupyter extension] which can work from existing Conda
environments without the need to manage a notebook server.

> [!TIP]
> This extension supports [notebook diffing].
>
> ![notebook diff example](https://code.visualstudio.com/assets/docs/datascience/jupyter/notebook-diffing.png)

[Python extension]: https://code.visualstudio.com/docs/languages/python
[Jupyter extension]: https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter
[notebook diffing]: https://code.visualstudio.com/docs/datascience/jupyter-notebooks#_custom-notebook-diffing


## Running R code

The Jupyter extension can also run R.

There is also an [R extension] which I haven't used, but seems to replicate many
features of RStudio.

![R extension example](https://code.visualstudio.com/assets/docs/languages/r/workspace-viewer.gif)

[R extension]: https://code.visualstudio.com/docs/languages/r


## Source Control++

Built-in source control features can be augmented by installing extensions.
These are the ones I have used extensively, but there are many others.

- [GitLens] - blame, graph, interactive rebase editor, and many other features
  (some are paid)
- [Open in GitHub] - handy for copying a link to specific lines

[GitLens]: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
[Open in GitHub]: https://marketplace.visualstudio.com/items?itemName=sysoev.vscode-open-in-github

<!-- DEMO

- show GitLens: Toggle File Blame
- show GitLens: Focus on Graph View
- show GitLens interactive rebase editor?
- show Open in GitHub: Copy File URL

-->


## Reviewing pull requests

The GitHub website can be difficult to navigate for pull requests with many
comments/conversations. The [GitHub Pull Requests] extension has a **Comments**
view with basic abilities to group and filter conversation threads.

It's also nice to see changes with the entire file contents as context, add
comments on changed lines without leaving the editor, and use familiar text
editor features in the review process.

[GitHub Pull Requests]: https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github

<!-- DEMO

- show https://github.com/nextstrain/augur/pull/1094

-->


## Programming with LLMs

If you're using a large language model (LLM) for programming assistance (e.g.
ChatGPT), you may find [GitHub Copilot] useful (free for students and teachers).
There is an extension available for VS Code among other editors.

[GitHub Copilot]: https://github.com/features/copilot

<!-- DEMO

- example commit: https://github.com/nextstrain/nextstrain.org/commit/aeba4db620cf64525bf31d9a264e7bd2c30f242b
- show how to do manually
- show how to do using Copilot
 
-->


## Final note

VS Code is just one of many text editors. At the time of writing this guide, a
[majority] of people in the lab are using it. This may be partly due to
Microsoft's power and influence. There are many other editors out there!

I've always used "visual" text editors where stuff can be done by clicking
around with a mouse. Over time, I've found myself using keyboard shortcuts more
often, and acknowledge that this is the strong point of terminal-based text
editors (e.g. emacs, nano, vim). Now, I use [VSCodeVim] to learn vim's
keybindings while still having access to all the visual features¹ available with
VS Code.

¹ features that [just keep coming]! Within 1 month from 17 May 2024, the VS Code
GitHub repository had 568 PRs merged by 51 people, according to [repo insights].

[majority]: https://bedfordlab.slack.com/archives/C0A0ASW4C/p1718144399045329
[VSCodeVim]: https://github.com/VSCodeVim/Vim
[just keep coming]: https://code.visualstudio.com/updates
[repo insights]: https://github.com/microsoft/vscode/pulse


## Other resources

- [Visual Studio Code docs](https://code.visualstudio.com/docs)
- [Visual Studio Code YouTube channel](https://www.youtube.com/@code)
