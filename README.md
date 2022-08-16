# inngest/action-test-functions

This action installs the Inngest CLI ([inngest/inngest](https://github.com/inngest/inngest)) on your Linux, Mac, or Windows runner in GitHub Actions, then tests the given Inngset function against generated, snapshotted, or real production data.

See also:

- [inngest/action-deploy-functions](https://github.com/inngest/action-deploy-functions)

## Usage

### Test using generated data

```yaml
steps:
  - uses: actions/checkout@v3
  - uses: inngest/action-test-functions@v1
```

There are a few options you can provide:

- `version` - the version of Inngest to use. Defaults to the latest version.
- `function` - the name of the function to test. Defaults to the current directory.
- `replay` - if true, we'll replay events from your [Inngest Cloud](https://www.inngest.com) account. Defaults to false.
- `snapshot` - the path to a snapshot file to use, generated using `inngest run --snapshot`. Defaults to empty (`""`).
- `prod` - if true and replay is true, we'll use the production data from your [Inngest Cloud](https://www.inngest.com) account. Defaults to false, meaning we'll use your test workspace.
- `token` - the auth token to use to authenticate with your [Inngest Cloud](https://www.inngest.com) account. Required if using `replay`.

### Test `./foo` using production replay

```yaml
steps:
  - uses: actions/checkout@v3
  - uses: inngest/action-test-functions@v1
    with:
      token: ${{ secrets.INNGEST_AUTH_TOKEN }}
      function: ./foo
      replay: true
      prod: true
```

### Test using a snapshot

```yaml
steps:
  - uses: actions/checkout@v3
  - uses: inngest/action-test-functions@v1
    with:
      snapshot: ./snapshot.json
```

