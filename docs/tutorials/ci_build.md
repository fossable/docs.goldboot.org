## Building Golden Images with CI

`goldboot` is designed to work on CI platforms like GitHub Actions, Travis CI, etc.

### GitHub Actions

```yaml
name: build
on:
  push:
    branches: [master]

jobs:
  build:
    name: Build Linux
    runs-on: ubuntu-latest
    steps:
      - name: Build image
        uses: goldboot/build-action@v1
        with:
          toolchain: nightly
          override: true
          components: rust-src
```