# git-push-action

Commit all modified files and push to the repository.

<!-- actdocs start -->

## Description

This action commits changes made during the workflow run and pushes them to a remote repository.
It supports specifying a branch name, a start point, multi-line commit messages, and allows creating empty commits.

## Usage

### Default

```yaml
  steps:
    - name: Git Push
      uses: tmknom/git-push-action@v0
      with:
        message: add useful feature
```

### Custom

```yaml
  steps:
    - name: Git Push
      uses: tmknom/git-push-action@v0
      with:
        message: add useful feature
        branch: new-feature-branch
        start-point: origin/main
        allow-empty: true
```

## Inputs

| Name | Description | Default | Required |
| :--- | :---------- | :------ | :------: |
| message | The commit message. | n/a | yes |
| allow-empty | Set to true to allow creating empty commits. | `false` | no |
| branch | Specify the name for the new branch. | n/a | no |
| paths | Space-separated list of file paths to add before committing. Supports glob patterns such as `*.md` or `docs/*.txt`. If not specified, all changes are added (equivalent to `.`). | n/a | no |
| start-point | The starting point for the new branch, allowing creation from a different commit than `HEAD`. | `HEAD` | no |

## Outputs

| Name | Description |
| :--- | :---------- |
| body | The body of the commit message (everything after the first line). |
| branch | Name of the pushed branch. |
| pushed | Whether the changes pushed to the repository. |
| subject | The first line of the commit message. |

<!-- actdocs end -->

## Permissions

| Scope    | Access |
| :------- | :----- |
| contents | write  |

## FAQ

### Where is the push destination if no branch is specified?

If no branch is specified, a uniquely named branch will be automatically created for each workflow run.

### What should I specify for `start-point`?

Usually, you should specify a remote tracking branch like `origin/main`, because local branches might not exist in GitHub Actions environments.
By default, `HEAD` is used, meaning the new branch will be created from the currently checked-out commit.

### Do I need to fetch branches manually when using `start-point`?

When using `start-point`, the base branch must exist in your local Git repository.
In GitHub Actions environments, by default, only a shallow clone with limited history is performed (`fetch-depth: 1`).
You may need to explicitly fetch the base branch using a command like:

```bash
git fetch origin main
```

or configure `actions/checkout` with:

```yaml
- uses: actions/checkout@v4
  with:
    fetch-depth: 0
```

to retrieve the complete branch history.

### What happens if there are no changes?

Normally, if there are no changes, no commit or push will occur.
However, if you set `allow-empty: true`, an empty commit will be created even when there are no changes.

### Can I specify which files to commit?

Yes. You can specify the files to add before committing by using the `paths` input.
It accepts a space-separated list of file paths, and supports glob patterns such as `*.md` or `docs/*.txt`.
If not specified, all changes are added (`.`) by default.

### Can I specify a multi-line commit message?

Yes. You can specify a multi-line commit message by using YAML's block scalar style (`|`),
which preserves newlines as part of the string.
For example:

```yaml
with:
  message: |
    First line of subject
    Second line of body
    Third line of body
```

The first line will be treated as the commit subject, and the following lines as the commit body.

### Can I push to an existing branch?

Currently, the implementation assumes pushing to a newly created branch.
If you attempt to push to an existing branch, a Git command error such as "branch already exists" may occur.

### What happens if an error occurs during Git operations?

If a Git operation such as `switch`, `commit`, or `push` fails,
the action will output a detailed error message and fail immediately.
The error message includes the Git command's stderr output for easier debugging.

## Related projects

- [git-config-action](https://github.com/tmknom/git-config-action): Configure the bot account in Git.
- [traceable-identifier-action](https://github.com/tmknom/traceable-identifier-action): Generate traceable identifier optimized for GitHub Actions.

## Release notes

See [GitHub Releases][releases].

[releases]: https://github.com/tmknom/git-push-action/releases
