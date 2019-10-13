# Sroka Package

Sroka is a Python package providing a developer-centric API to fetch data from multiple sources:

* Google Analytics
* Google AdManager (GAM earlier DoubleClick for Publishers, DFP)
* MOAT
* Qubole
* Rubicon
* Athena
* Google sheets
* s3
* MySQL

## Developers

Install the requirements and enable custom git-hooks:

```bash
pip install -r requirements.txt
git config --local core.hooksPath .githooks/
```

Check that the code is properly formatted by using `flake8` from the root of the repository:

```bash
flake8 .
```

## Installation

### Pypi last release

In order to get the last stable release, run the following command:

```bash
pip install sroka
```

### GitHub version (beta version)

In order to get the current beta version, run the following command:

```bash
pip install git+ssh://git@github.com/Wikia/sroka
```

## Configuration

In your home folder, create a hidden folder named `.sroka_config` where to store:

* The `config.ini` file, based on `config.sample.ini` with information to access your data source(s)
* For Google Analytics, a file named [`client_secrets.json`](#google-analytics) is also required
* For Google Ad Manager, a file named [`ad_manager.json`](#gam) is also required

Alternatively, you can set a custom localization for those files when importing Sroka:

```python
from sroka.config.config import setup_env_variables
from sroka.config.config import setup_client_secret
from sroka.config.config import setup_admanager_config

setup_env_variables('/path/to/config.ini')
setup_client_secret('/path/to/client_secrets.json')
setup_admanager_config('/path/to/ad_manager.json')
```

## How to get the Google JSON files

### Google Analytics

1. Use [this wizard](https://console.developers.google.com/flows/enableapi?apiid=analytics.googleapis.com) 
to create or select a project in the **Google Developers Console** and automatically turn on the API. Click `Continue`, then `Go to credentials`.
2. On the `Add credentials to your project` page, click the `Cancel` button.
3. At the top of the page, select the `OAuth consent screen` tab. Select an email address, enter a product name if it's not already set, and click the `Save` button.
4. Select the `Credentials` tab, click the `Create credentials` button and select `OAuth client ID`.
5. Select the application type `Other`, enter the chosen name, and click the `Create` button.
6. Click `OK` to dismiss the resulting dialog.
7. Click the `Download JSON` button to the right of the client ID.

### Google Ad Manager

1. Follow [these instructions](https://developers.google.com/ad-manager/api/authentication#service) -- while adding a service account, note that the role needs to have the necessary viewing and reporting permissions. You should end up with a JSON file containing your credentials credentials.
2. Make sure the `Name` in "OAuth 2.0 client IDs" matches the `service account` in "Service account keys" on [this page](https://console.developers.google.com/apis/credentials).
4. Create a Google Ad Manager account as a service account, not a new user, by following [those instructions](https://support.google.com/admanager/answer/6078734?hl=en).
3. Once you have a service account, it can be used to fetch data from different networks. Simply add your new service account to other networks through the Google Ad Manager UI.
4. Additional information can be specified in the `config.ini` file:
    1. `network code`: the ID of your network. A default value that can be overwritten in a function call
    2. `application name`: the custom name of your network. If not specified, a generic value will be passed.

### Google Sheets

[Follow this link](https://developers.google.com/sheets/api/quickstart/python) and click the button
`ENABLE THE GOOGLE SHEETS API` to create a project with access to Google Sheets. You should
end up with `credentials.json` file that you can download and put in your `~/.sroka_config` folder.

## How to get Qubole and Athena Access Tokens

### Qubole

1. Find your Qubole API Token (go to `User` -> `My Profile` -> `my_account` -> `API Token` -> `show`)
2. Copy your the token to in the `config.ini` file, in the `[quoble]` section, to the right of `api_token:`.

Example:

```ini
[qubole]
api_token: 938f6d8-098abc87-468c90d-986e78f
```

### Athena and S3

1. You should have your aws_access_key_id and aws_secret_access_key from registration process in AWS console.
2. s3bucket_name can be found in AWS console in Athena view when you click `Settings`, there you have `Query result location`.
The name of location without `s3://` and `/` is what you need.
3. For Athena usage you need to set also region (AWS regional endpoint), e.g. `'us-east-1'`

### Rubicon

1. You should have your `id`, `username` and `password` from Rubicon
2. Set the values accordingly in the `config.ini` file, in the `[rubicon]` section

Example:

```ini
[rubicon]
username: example
password: strongpassword
id: 938f6d8-098abc87-468c90d-986e78f
```

## Others

### MySQL

1. In order to connect to a remote MySQL server, you need to provide the `host` and `port` values in the configuration. If it is accessible through a unix socket, you need to provide the path to this socket instead in the `unix_socket` configuration field.
2. If the MySQL server is protected by user credentials, you need to provide the `user` and `password` values in the configuration.
3. You can optionally specify the database to which you want to connect in the `database` configuration field.

Example:

```ini
[mysql]
host: 1.2.3.4
port: 4742
username: example
password: strongpassword
database: users
```

## Common issues

### macOS

If you see the error `ValueError: unknown locale: UTF-8`, please export the following environment variables in your shell:

```bash
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

### Installing Sroka

1. If the `PyYAML` package is not building correctly, it might be because recent versions of `pip` won’t uninstall the package because it’s handled by `disutils`. Please install the `PyYAML` package first, with the additional `--ignore-installed` flag. 
2. If `numpy` gets messed up during Sroka's installation, it is probably caused by having multiple conflicting versions installed. Please uninstall all dependencies using `pip uninstall` and then reinstall the latest ones.

## Credits

All people that contributed to Sroka's development, also before going open source (including CR and QA):

* [martynaut](https://github.com/martynaut)
* [dorotamierzwa](https://github.com/dorotamierzwa)
* [fraszczakszymon](https://github.com/fraszczakszymon)
* [bckatarzyna](https://github.com/bckatarzyna)
* [jacekbj](https://github.com/jacekbj)
* [nandy-andy](https://github.com/nandy-andy)
* [dmnsobczak](https://github.com/dmnsobczak)
* [szczeles](https://github.com/szczeles)
* [kvas-damian](https://github.com/kvas-damian)
* [pnather](https://github.com/pnather)
* [philthyharry](https://github.com/philthyharry)
