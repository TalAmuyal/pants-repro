python_sources(
    name="pacifica-db-src-sources",
    sources=["pacifica/**/*.py"],
)

resource(name="pyproject", source="pyproject.toml")

python_distribution(
    name="pacifica-db",
    dependencies=[
        ":pyproject",
        ":pacifica-db-src-sources",
        # Dependencies on code to be packaged into the distribution.
    ],
    provides=python_artifact(
        name="pacifica-db",
        version="2.21.0",
    ),
    wheel_config_settings={"--global-option": ["--python-tag", "py37.py38.py39"]},
    generate_setup=True,
    sdist=False,
    wheel=True,
)
