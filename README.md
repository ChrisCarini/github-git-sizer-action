# git-sizer GitHub Action

A [GitHub Action](https://help.github.com/en/actions) for executing [github/git-sizer](https://github.com/github/git-sizer).

[![GitHub Marketplace](https://img.shields.io/github/v/release/ChrisCarini/github-git-sizer-action?label=Marketplace&logo=GitHub)](https://github.com/marketplace/actions/git-sizer)
[![GitHub Marketplace](https://img.shields.io/github/contributors/ChrisCarini/github-git-sizer-action?label=Contributors&logo=GitHub)](https://github.com/ChrisCarini/github-git-sizer-action/graphs/contributors)
[![GitHub Marketplace](https://img.shields.io/github/release-date/ChrisCarini/github-git-sizer-action?label=Last%20Release&logo=GitHub)](https://github.com/ChrisCarini/github-git-sizer-action/releases)
[![All Contributors](https://img.shields.io/github/all-contributors/ChrisCarini/github-git-sizer-action?color=ee8449&style=flat-square)](#Contributors)

# Usage

Add the action to your [GitHub Action Workflow file](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow#creating-a-workflow-file) - the only thing you _need_ to specify is the action itself.

A minimal example of a workflow step is below:
```yaml
  - name: Run git-sizer
    uses: ChrisCarini/github-git-sizer-action@latest
```

## Installation

1) Create a `.yml` (or `.yaml`) file in your GitHub repository's `.github/workflows` folder. We will call this file `git-sizer.yml` below.
2) Copy the below contents into `git-sizer.yml`
    ```yaml
    name: Analyze Repo with git-sizer
    
    on:
      schedule:
      - cron: '0 0 * * 0'  # Runs on Sundays at midnight UTC; https://crontab.guru/#0_0_%2A_%2A_0
    
    jobs:
      run-git-sizer:
        name: git-sizer - ${{ github.event.inputs.repo }}
        runs-on: ubuntu-latest
        steps:
          - name: Run git-sizer
            uses: ChrisCarini/github-git-sizer-action@latest
    ```

## Options

This GitHub Action exposes 3 input options, only one of which is required.

|  Input  | Description                                                                                                                       |   Usage    |                     Default                     |
|:-------:|:----------------------------------------------------------------------------------------------------------------------------------|:----------:|:-----------------------------------------------:|
| `repo`  | The repository to run `git-sizer` against.                                                                                        | *Optional* | `"https://github.com/${{ github.repository }}"` |
| `flags` | Any additional flags that are desired to be passed to the `git-sizer` invocation. Check `git-sizer --help` for available options. | *Optional* |                     _None_                      |

An example using **_ALL_** the available options is below:
```yaml
    - name: Run git-sizer
      uses: ChrisCarini/github-git-sizer-action@latest
      with:
        repo: "https://github.com/ChrisCarini/github-git-sizer-action"
        flags: "--threshold=0"
``` 

### `repo`

This optional input allows users to specify a different repository to run `git-sizer` against.

### `flags`

This optional input allows users to specify flags or options to be used when invoking `git-sizer` in this GitHub Action. The default is no flags.

## Results

The output of the `git-sizer` execution is captured in an output variable for use in subsequent steps, if you so choose.

You will need to give the `github-git-sizer-action` step an `id`.

You can then access the output of `git-sizer` by using `${{steps.<id>.outputs.result}}`.

In the below example, we use set the `id` to `sizer` - this example will print the filename as well as the contents of the file as a subsequent step to the validation:

```yaml
      - name: Run git-sizer
        id: sizer
        uses: ChrisCarini/github-git-sizer-action@latest

      - name: Print git-sizer output to a file
        run: |
          printf "%s\n" "${{ steps.sizer.outputs.result }}" > this-file-has-git-sizer-output.txt
          cat this-file-has-git-sizer-output.txt
```

# Examples

As examples of using this plugin you can check out following projects:

- **_this repository!_**
  - `.github/workflows/workflow_dispatch.yml` - A workflow using `workflow_dispatch` trigger to run against a repo from user input (🔗 [link](https://github.com/ChrisCarini/github-git-sizer-action/blob/main/.github/workflows/workflow_dispatch.yml)).
  - `.github/workflows/workflow_schedule.yml` - A workflow scheduled to run on Sunday at 00:00UTC to run against **this** repo (🔗 [link](https://github.com/ChrisCarini/github-git-sizer-action/blob/main/.github/workflows/workflow_schedule.yml)).

# Contributing

Contributions welcomed! Feel free to open a PR, or issue.

## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/ChrisCarini"><img src="https://avatars.githubusercontent.com/u/6374067?v=4?s=100" width="100px;" alt="Chris Carini"/><br /><sub><b>Chris Carini</b></sub></a><br /><a href="#bug-ChrisCarini" title="Bug reports">🐛</a> <a href="#code-ChrisCarini" title="Code">💻</a> <a href="#doc-ChrisCarini" title="Documentation">📖</a> <a href="#example-ChrisCarini" title="Examples">💡</a> <a href="#ideas-ChrisCarini" title="Ideas, Planning, & Feedback">🤔</a> <a href="#maintenance-ChrisCarini" title="Maintenance">🚧</a> <a href="#question-ChrisCarini" title="Answering Questions">💬</a> <a href="#review-ChrisCarini" title="Reviewed Pull Requests">👀</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
