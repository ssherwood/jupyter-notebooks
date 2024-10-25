# Jupyter Notebooks

Collection of my personal Jupyter Notebooks

## Requirements

* [Bash Kernel](https://github.com/takluyver/bash_kernel)

## Jupyter Notebooks and Secrets

Notebooks can leak a lot of information that could be considered secret. In general, this project uses a local `.env` file in each folder used to store secret information like passwords or API keys.

This project also uses a special git configuration option to effectively clear the output before pushing to GitHub. Specifically, in the `.git\config` file:

```shell
[filter "strip-notebook-output"]
    clean = "jupyter nbconvert --ClearOutputPreprocessor.enabled=True --ClearMetadataPreprocessor.enabled=True --to=notebook --stdin --stdout --log-level=ERROR"
    smudge = "cat"
    required
```

Also added is an `attributes` file to `.git/info`:

```shell
*.ipynb filter=strip-notebook-output
```

This effectively runs `nbconvert` on each notebook and clears the output from previous executions, thus limiting potentially leaking secret information from console output.
