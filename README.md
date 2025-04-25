# git-push-action

Commit all modified files and push to the repository.

<!-- actdocs start -->

## Description

This action creates a new commit and pushes the changes back to the remote repository.
It automatically commits files that were modified during the workflow run.

## Usage

```yaml
  steps:
    - name: Git Push
      uses: tmknom/git-push-action@v0
      with:
        message: add useful feature
```

## Inputs

| Name | Description | Default | Required |
| :--- | :---------- | :------ | :------: |
| message | The commit message. | n/a | yes |
| allow-empty | Set to true to allow creating empty commits. | `false` | no |
| branch | Specify the name for the new branch. | n/a | no |
| start-point | The starting point for the new branch, allowing creation from a different commit than `HEAD`. | `HEAD` | no |

## Outputs

| Name | Description |
| :--- | :---------- |
| branch | Name of the pushed branch. |
| pushed | Whether the changes pushed to the repository. |
| subject | The first line of the commit message. |

<!-- actdocs end -->

## Permissions

| Scope    | Access |
| :------- | :----- |
| contents | write  |

## FAQ

N/A

## Related projects

- [git-config-action](https://github.com/tmknom/git-config-action): Configure the bot account in Git.
- [traceable-identifier-action](https://github.com/tmknom/traceable-identifier-action): Generate traceable identifier optimized for GitHub Actions.

## Release notes

See [GitHub Releases][releases].

[releases]: https://github.com/tmknom/git-push-action/releases
