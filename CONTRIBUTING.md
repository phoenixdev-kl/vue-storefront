# How to Contribute

Already a JavaScript/Vue.js developer? Pick an issue, create a pull request and instantly become a member of the vue-storefront contributors community. We've marked some issues as `Easy first pick` to make it easier for newcomers to begin!

Thank you for your interest in, and engagement!

Before you submit an issue please read about our [release lifecycle](docs/guide/basics/release-cycle.md).

## Branches

You should fork the project or create a branch for new features. The main branches used by the core team are:

- `master` - where we store the stable release of the app (that can be deployed to our demo instances),
- `develop - the most recent version of the app - kind of "nightly" build.
- RC-x (`x` is current version) - release candidate branch with features that will land in next version.

Please use `develop` or `RC` for development purposes as the `master` can be merged just as the new release is coming out (about once a month).

## Issue reporting guidelines

Always define the type of issue:

- Bug report
- Feature request

While writing issues, please be as specific as possible. All requests regarding support with implementation or application setup should be sent to [contributors@vuestorefront.io](mailto:contributors@vuestorefront.io)

If the issue is about some changes with a particular theme, please prefix the issue with theme name (ex. `[default] change product tile background color`).

**Tag your issues properly**. If you found a bug tag it with `bug` label. If you're requesting new feature tag it with `feature request` label.

## TypeScript

We're introducing TypeScript to Vue Storefront core, so you can use it where it's appropriate - but please be pragmatic. Would be nice to TypeScript features only in new modules and Vuex.
Here are some thoughts on how to use TypeScript features in Vue Storefront: [TypeScript Action Plan](typescript.md).

## Pull request checklist

Here’s how to submit a pull request. **Pull requests not meeting these requirements won't get merged.**.

::: warning
**ALWAYS** use the [pull request template](.github/PULL_REQUEST_TEMPLATE.md), it's automatically added to each pull request.
:::

1. Fork the repository and clone it locally from the `develop` branch. Make sure it's up to date with current `develop` branch.
2. Create a branch for your edits. Use the following branch naming conventions:

- `bugfix/task-title`
- `feature/task-name`

3. Use pull request template and fill as much fields as possible to describe your solution.
4. Reference any relevant issues or supporting documentation in your pull request (ex. "Issue: 39. Issue title.").
5. If you are adding a new feature, please provide documentation along with the pull request. Also, add it to [upgrade notes](docs/guide/upgrade-notes/README.md).
6. If you are removing/renaming something or changing its behavior, please also include it in [upgrade notes](docs/guide/upgrade-notes/README.md).
7. Test your changes! Run your changes against any existing tests and create new ones when needed. Make sure your changes don’t break the existing project. Make sure that your branch is passing Travis CI build.
8. If you have found a potential security vulnerability, please _do not_ report it on the public issue tracker. Instead, send it to us at [contributors@vuestorefront.io](mailto:contributors@vuestorefront.io). We will work with you to verify and fix it as soon as possible.
([README.md#documentation--table-of-contents](README.md#documentation--table-of-contents))

## Acceptance criteria

Your pull request will be merged after meeting following criteria:
- Everything mentioned in [Pull request checklist](#pull-request-checklist)
- Pull request is proposed to appropriate branch 
- There are at least two approvals from core team members
