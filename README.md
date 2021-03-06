# freshsales-sdk-py

Unofficial Python SDK for accessing [Freshsales](https://www.freshsales.io/api/).

*Warning*: This is undergoing active development and we will accept contributions once things are a little stable.

## Installation

1. Download this project and use it (copy it in your project, etc).
2. Install it from [pip](https://pypi.org).

```
pip install freshsalessdk
```

## Usage

To use this SDK you'll need these Freshsales credentials and your Freshsales domain (https://domain.freshsales.io). See [official documentation](https://www.freshsales.io/api/#intro) for steps. We'll assume these are available via environment variables thusly:

```
export FS_API_KEY=xxx
export FS_DOMAIN=yyy
```

The following snippet shows you how to initialize and use the SDK.

```python
from freshsalessdk import FreshsalesSDK
import os

fs = FreshsalesSDK(
    domain=os.getenv('FS_DOMAIN'),
    api_key=os.getenv('FS_API_KEY')
)

# get contact views
contact_views = fs.contacts.get_views()

# get contacts in a view
view_id = contact_views[0]['id']
contacts = fs.contacts.get_all(view_id=view_id)
contacts = list(fs.contacts.get_all_generator(view_id=view_id))

# get specific contact
contact_id = 1232
contact = fs.contacts.get(id=contact_id)

# get contact activities
activities = fs.contacts.get_activities(id=contact_id)

# get account views
account_views = fs.accounts.get_views()

# get accounts in a view
view_id = account_views[0]['id']
accounts = fs.accounts.get_all(view_id=view_id)
accounts = list(fs.accounts.get_all_generator(view_id=view_id))

# get one account
account_id = 1221
account = fs.accounts.get(id=account_id)

# get deal views
deal_views = fs.deals.get_views()

# get deals in a view
view_id = deal_views[0]['id']
deals = fs.deals.get_all(view_id=view_id)
deals = list(fs.deals.get_all_generator(view_id=view_id))

# get single deal
deal_id = 12121
deal = fs.deals.get(id=deal_id)

# get lead views
lead_views = fs.leads.get_views()

# get leads in a view
view_id = lead_views[0]['id']
leads = fs.leads.get_all(view_id=view_id)
leads = list(fs.leads.get_all_generator(view_id=view_id))

# get single lead
lead_id = 121212
lead = fs.leads.get(id=lead_id)
```

## Code-hygiene, Tests and Code Coverage

To ensure that coding styles are followed, run the following command:
```
pylint --rcfile=.pylintrc freshsalessdk test
```

To run integration tests, you'll need to set FS_DOMAIN and FS_API_KEY environment variables. In addition, you should have
a view with all objects "All Contacts" for contacts and similarly "All Accounts" for accounts and "All Deals" for deals. Then simply run:

```
python -m pytest
```

To get code coverage, run the tests thusly. 

```
python -m pytest --cov=freshsalessdk
```

Which produces output like this:

```
---------- coverage: platform darwin, python 3.7.4-final-0 -----------
Name                             Stmts   Miss  Cover
----------------------------------------------------
freshsalessdk/__init__.py            3      0   100%
freshsalessdk/freshsalessdk.py     130      6    95%
----------------------------------------------------
TOTAL                              133      6    95%
```

We want to maintain more than 90% code coverage. To get lots of debugging data during tests, edit the pytest.ini file.

To get code coverage report in HTML, run this command:

```
python -m pytest --cov=freshsalessdk --cov-report html:cov_html
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
