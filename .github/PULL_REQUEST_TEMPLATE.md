<!-- Thanks for contributing to HZLib! Fill this out before requesting review. -->

## What Does This PR Do?

<!-- A clear one-line summary. -->

## Why?

<!-- What problem does this solve, or what does it enable? Link to a related issue if one exists. -->
Closes #

## How Has This Been Tested?

<!-- Which loader(s) and MC version(s) did you test on? -->

- [ ] Fabric — MC `___`
- [ ] Forge — MC `___`
- [ ] NeoForge — MC `___`

<!-- Describe the test case briefly. -->

## Type of Change

- [ ] Bug fix
- [ ] New feature / API addition
- [ ] Refactor (no behaviour change)
- [ ] Breaking change (modifies existing public API)
- [ ] Documentation only
- [ ] Build / config change

## Checklist

- [ ] All three loaders build without warnings
- [ ] Follows the [Coding Style Guide](docs/guidelines/Coding%20Style%20Enforcer.md) — JavaDoc on all public API
- [ ] Commit messages follow [GIT_COMMIT_GUIDELINES](docs/guidelines/maintenance/GIT_COMMIT_GUIDELINES.md)
- [ ] `CHANGELOG.md` updated if this adds or changes public API
- [ ] No new string literals used as NBT keys — `DataField<T>` handles only
- [ ] If adding a new `DataField<T>`, a `MigrationStep` is included or justified as not needed
