# Contributing to calcite-design-tokens

You want to contribute? Nice! Below are some guidelines for ensuring that your contribution makes sense for everybody.

## Reporting Issues

Found a problem? Want a new feature?

- See if your issue or idea has [already been reported](issues).
- Provide detailed reproduction instructions as well as what behavior is expected.

## Submitting Pull Requests

Pull requests are the greatest contributions, so be sure they are focused in scope.

1. To begin, [fork this project](fork), clone your fork, and add our upstream.

```bash
# Clone your fork of the repo into the current directory
git clone https://github.com/<your-user>/calcite-design-tokens
# Navigate to the newly cloned directory
cd calcite-design-tokens
# Assign the original repo to a remote called "upstream"
git remote add upstream https://github.com/esri/calcite-design-tokens
# Install the tools necessary for development
npm install
```

2. Create a branch for your feature or fix:

```bash
# If you are a designer setting up a branch for FigmaTokens Plugin, make sure your branch name starts with `designer/`.
git checkout -b designer/[yourname]
```

```bash
# Use the calcite default branching pattern
git checkout -b [yourname]/[type]-[issue#]
```

3. Be sure your code follows our practices.

```bash
# Test current code
npm run test
```

4. Push your branch up to your fork:

```bash
# Push a designer branch
git push origin designer/[yourname]
```

```bash
# Push a developer branch
git push origin [yourname]/[type]-[issue#]
```

5. Now [open a pull request](https://help.github.com/articles/using-pull-requests/) with a clear title and description.

## Bumping the Version

1. Following the rules of [SEMVER](https://semver.org/), change the version number in `package.json` to the appropriate version number.
2. Write a description of the changes, additions, and bug fixes in `CHANGELOG.md`.
3. Run `npm run build` to make sure the `build/` files are updated.
4. Make sure `Esri/calcite-design-tokens` is up-to-date with your changes (via Pull Request).
5. Run `npm run release`. If prompted enter your GitHub credentials.

## CI Automation

Github actions facilitate the token handoff between the Designers using the Figma Tokens Plugin and a multi-branch git repo.

Designers using the Figma Token Plugin should set their watched git repo to `designers/[custom-name]`.

### design-tokens-pr.yml

This file allows designers to each work off their own branch. Helping prevent accidental overwrites from other people working on the same tokens files.

Automated Steps

1. Watches for changes to any branch in the repo named `designers/*`.
1. Generate a pull request with new changes to the set feature branch.

### Wait for reviewers

Await reviews from the team before merging the new work from designers into the feature branch. This allows time for discussion and alignment on bug fixes, features, and potential breaking changes before merging.

### design-tokens-sync.yml

When changes are detected on the feature branch, generate a pull-request back to the designer branches. This avoids the burden on designers to have to switch between branches in the Figma Token plugin and ensuring any conflicts between each designer's branch and the feature branch do not accidentally overwrite the designers work.

Automated Steps

1. Watch for changes on the feature branch.
1. Open pull-requests to each of the designer branches set in the action file.
1. Add `automated-tokens-pr'` label.

### design-tokens-automerge.yml

Auto merge pull requests created with the label `automated-tokens-pr`.

Automated Steps

1. Watch for pull requests with the label `automated-tokens-pr`.
1. Wait to confirm the pull request passes required checks.
1. Merge the pull request with the commit message `chore: automatic merge`.
