# Echo VR API

Python bindings for Echo VR's HTTP API.

## Installation

If you haven't already, [install Python 3](https://www.python.org/downloads/) and [Pipenv](https://pipenv.readthedocs.io/en/latest/install/).

Now, in your project directory, run:

```
pipenv install echovr-api
```

## Usage Example

```
from requests.exceptions import ConnectionError
import json
import echovr_api

try:
    game_state = echovr_api.fetch_state()

    print(f"Game status: {game_state.game_status}")
    print(f"Seconds on clock: {game_state.game_clock}")

    if (game_state.blue_team.score > game_state.orange_team.score):
        print("Blue team is winning!")
    elif (game_state.orange_team.score > game_state.blue_team.score):
        print("Orange team is winning!")
    else:
        print("It's tied!")

    print(f"Score: {game_state.blue_team.score} - {game_state.orange_team.score}")

except ConnectionError as e:
    print("Connection refused. Make sure you're running Echo VR with the -http option and that you're in a match.")
except json.decoder.JSONDecodeError as e:
    print("Could not decode response. (Not valid JSON.)")
```

For full documentation of the available methods and classes, feel free to browse the docstrings in the source code.

## Contributing

To get everything you need to start making changes to this package, first [install Python 3](https://www.python.org/downloads/) and [Pipenv](https://pipenv.readthedocs.io/en/latest/install/), clone this repository, then run:

```
pipenv install
```

### Try it

To play around with the API, open an instance of Echo VR with the -http flag, then run:

```
pipenv run python -i ./test.py
```

### Release process

First, update `CHANGELOG.md` and the version number in `setup.py`. Commit, tag,
and push these changes.

Next, build the package:

```
pipenv install --dev
pipenv run python setup.py sdist bdist_wheel
```

Finally, upload the built packages to PyPi. You can do this using `twine`
(`pip install twine`):

```
twine upload dist/*
```
