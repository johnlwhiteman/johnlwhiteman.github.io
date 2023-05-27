# Mkdocs

Here we show how to get started with `mkdocs`. We are going to be publishing on GitHub's GitPages using a dedicated domain that they provide for us free.

## Installation

* Install the latest python and git on your device
* Log in to [GitHub](https://github.com/)
* Create a new GitHub repo using the naming convention: `<your github id>.github.io`
    * e.g., `johnlwhiteman.github.io`
* Run the following commands on your device

```bash
git clone <repo>
cd <repo>
pip install mkdocs
pip install mkdocs-material
pip install mkdocs-mermaid2-plugin
pip install mkdocs-charts-plugin
mkdocs new .
mkdocs serve
```

* Verify that everything is working. Open a browser and navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000)

## Setting Up GitHub Actions

* Create the following directories under the parent repo directory
    * This directory will contain the GitHub actions assets

```bash
mkdir -p .github/workflows
```

* Create a new GitHub Actions file
    ./github/workflows/ci.yml
* Copy the contents the [GitHub Actions File](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#material-for-mkdocs) provided by mkdocs.

```
name: ci
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
      - uses: actions/cache@v3
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

## Deployment

Since we have GitHub Actions enabled, deployment to GitPages is automatic

```bash
git add --all
git commit -s -m "Me comments"
git push origin main
```




## Build

```bash
mkdocs build
```

## Deploy


## References
* [GitHub](https://github.com/squidfunk/mkdocs-material)
* [GitHub Pages](https://squidfunk.github.io/mkdocs-material/getting-started/)
* [Website](https://www.mkdocs.org/)
* [Best of mkdocs](https://github.com/mkdocs/best-of-mkdocs)
* [Mermaid2](https://github.com/fralau/mkdocs-mermaid2-plugin)
* [Drawio](https://github.com/LukeCarrier/mkdocs-drawio-exporter)
* [Charts](https://github.com/timvink/mkdocs-charts-plugin)
* [Vega-Lite Editor](https://vega.github.io/editor/#/)