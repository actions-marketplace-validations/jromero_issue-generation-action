# VERIFICATION

```shell
npm run prepare-for-pr
```

# RELEASE

1. Update all references to version
2. Run the following commands:
    ```shell
    npm login
    npm run prepare-for-pr
    npm publish
    ```
3. Commit changes
4. Tag and Release via GitHub
