# Jupyter Notebooks for YugabyteDB

This is a collection of Jupyter Notebooks for using YugabyteDB.

## Jupyter Notebooks and Secrets

Notebooks can leak a lot of information that could be considered secret. In general, this project uses a local `.env` file in each folder used to store secret information like passwords or API keys.

This project also uses a special git configuration option to effectively clear the output before pushing to GitHub. Specifically, in the `.git\config` file:

```shell
[filter "strip-notebook-output"]
    clean = "jupyter nbconvert --ClearOutputPreprocessor.enabled=True --ClearMetadataPreprocessor.enabled=True --to=notebook --stdin --stdout --log-level=ERROR"
    smudge = "cat"
    required
```

I also added an `attributes` file to `.git/info`:

```shell
*.ipynb filter=strip-notebook-output
```

This runs nbconvert on each checkout and clears the output from any of the previous runs limiting potentially leaking secret information from console output.