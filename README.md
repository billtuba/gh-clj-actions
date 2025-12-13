# gh-clj-actions

Reusable GitHub Actions for Clojure projects.

## Actions

### setup-env

Sets up a Clojure development environment with caching.

**Includes:**
- Checkout code
- Install Java (Temurin 24)
- Install Clojure CLI tools
- Cache Maven/Gitlibs dependencies

**Usage:**

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: billtuba/gh-clj-actions/setup-env@v1
    - name: Run tests
      run: clojure -M:test
```

**Cache Details:**
- Caches `~/.m2/repository`, `~/.gitlibs`, `.cpcache`
- Cache key based on `deps.edn` hash
- Speeds up subsequent workflow runs by ~25 seconds

## Versioning

- `@v1` - Latest v1.x.x release (recommended for stability)
- `@main` - Latest commit (cutting edge, may break)

## License

MIT
