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

## Outputs

| Name | Description |
| :--- | :---------- |
| branch | Name of the pushed branch. |
| pushed | Whether the changes pushed to the repository. |

<!-- actdocs end -->

## Permissions

| Scope    | Access |
| :------- | :----- |
| contents | write  |

## FAQ

N/A

## Related projects

- [git-config-action](https://github.com/tmknom/git-config-action): Configure the bot account in Git.

## Release notes

See [GitHub Releases][releases].

## License

Apache 2 Licensed. See [LICENSE](LICENSE) for full details.

[releases]: https://github.com/tmknom/git-push-action/releases
