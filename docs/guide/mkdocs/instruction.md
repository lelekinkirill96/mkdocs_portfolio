
```
source .venv/bin/activate
```

```
python3 -m pip install -r requirements.txt
```


```
mkdocs-material
```


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
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache 
          restore-keys: |
            mkdocs-material-
      - run: pip install -r requirements.txt
      - run: mkdocs gh-deploy --force
```

```
site_name: Lelekin
site_url: https://lelekinkirill96.github.io/mkdocs_portfolio/


theme:
  name: material
  font:
    text: Merriweather Sans
  icon:
    logo: fontawesome/solid/pen
  palette:
# dark mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Dark mode
      primary: green
      accent: deep purple 

# light mode
    - scheme: default
      toggle:
        icon: material/weather-night
        name: Light mode
      primary: blue
      accent: deep orange
  features:
    - navigation.footer
```
