# Yarn offline mirror bug with scoped packages

This repo is merely to reproduce a bug in `yarn` when using scoped packages.

## The bug

Scoped packages are not being added/removed in the offline mirror when `yarn-offline-mirror-pruning` is set to `true`.

In my tests the bug seems to only affect scoped packages, such as `@kadira/storybook`. Yarn simply ignores them in the offline mirror, `yarn.lock` seems fine though.

## Reproducing the bug

1) Clone this repo;

2) Make sure yarn is using the local `.yarnrc`;

3) Run `yarn install`;

4) The `.yarncache` does not contain `@kadira/storybook` package. It should be there.

## Details

You can see that normal packages like `react` and `react-dom` can be added or removed just fine and the offline mirror keeps synchronized.

Adding or removing scoped packages with `yarn add` and `yarn remove` doesn't seem to work. The offline mirror is not being updated accordingly.

## Workaround

Removing the `yarn-offline-mirror-pruning` config seem to workaround this bug, though you will not have automatic offline mirror cleaning then.

## Environment tested

This bug was found in `yarn` version 0.24.6, using `node` 7.2.2 on macOS `10.12.5`.
