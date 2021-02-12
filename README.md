# poetry-demo
A template for using Poetry to manage Python projects.


## Initializing an existing repo with Poetry
1. From the project root, run:

    ``` sh
    poetry init
    ```


2. Configure our private PyPI repository:

    ```sh
    poetry config repositories.daas https://daas-451344765713.d.codeartifact.us-east-2.amazonaws.com/pypi/pypi-store/simple/
    ```

    Here I am choosing to call this private repo `daas`. You can name it what ever you like, just make sure you configure auth for the same name in the next step.

    ```sh
    export CODEARTIFACT_AUTH_TOKEN=`aws codeartifact get-authorization-token --domain daas --domain-owner 451344765713 --query authorizationToken --output text`

    poetry config http-basic.daas aws $CODEARTIFACT_AUTH_TOKEN
    ```

    Our username is `aws` and the password is our token.


3. [Add dependencies](https://python-poetry.org/docs/basic-usage/#specifying-dependencies), either by:

    a. Moving packages listed in [`requirements.txt`](./requirements.txt) to the `[tool.poetry.dependencies]` section of[ `pyproject.toml`](./pyproject.toml) and run[`poetry install`](https://python-poetry.org/docs/basic-usage/#installing-dependencies), or
    
    b. Using the Poetry CLI:        

    ```sh
    poetry add PACKAGE_NAME
    ```


4. Use [`poetry run`](https://python-poetry.org/docs/basic-usage/#using-poetry-run) to operate within your project's virtual environment.

    e.g.

    ```sh
    poetry run python --version             # To get the Python version within your virtual environment

    poetry run pip install --upgrade pip    # To update your virtial environment's pip
    ```
