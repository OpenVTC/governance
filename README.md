# OpenVTC Governance

This repo manages the OpenVTC GitHub org with
[CLOWarden](https://github.com/cncf/clowarden). Teams, members, and repositories
are defined in `config.yaml`, and CLOWarden reconciles the live org state to
match.

## Making changes

1. Edit `config.yaml` on a branch.
2. Open a PR. CLOWarden posts a plan as a PR comment showing what will change
   (teams created, members added, repos updated, etc.).
3. Review the plan carefully — if it looks right, merge the PR.
4. CLOWarden applies the changes to the org after merge.

## Adding a new repository

Follow the convention already in `config.yaml`:

```yaml
- name: <repo-name>
  teams:
    openvtc-admins: admin
    openvtc-maintainers: maintain
  visibility: public
```

Match the team/permission pattern used by the other repos unless there's a
specific reason to differ — consistency keeps the org easy to audit.

### Gotcha: push `main` before CLOWarden runs

A brand-new GitHub repo has no default branch until you push one. If CLOWarden
tries to configure branch protection or other `main`-dependent settings on an
empty repo, it will fail. **Create the repo entry in `config.yaml`, then push an
initial commit to `main` promptly** (a README is enough) so the rest of the
configuration can apply cleanly.

## Things CLOWarden can't do

Some actions are out of scope for CLOWarden and require LF staff (the `lf-staff`
team) to perform directly. The most common one:

- **Deleting a repository.** Removing a repo from `config.yaml` does _not_
  delete it — it only causes CLOWarden to stop managing it. To actually delete a
  repo, contact lf-staff.

When in doubt about whether something needs lf-staff involvement, ask in the
usual channels before merging.
