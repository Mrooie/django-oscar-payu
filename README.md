# django-oscar-payu #

Following are the configurations required for setting up django-oscar-payu

### Installation ###

`pip install django-oscar-payu`

### Getting Started ###

Add `payu` to installed apps.


Add the following to the `setting.py` file of your django-oscar setup:

```python
PAYU_INFO = {
    'INR': {
        'merchant_key': "gtKFFx",
        'merchant_salt': "eCwWELxi",
        # for production environment use 'https://secure.payu.in/_payment'
        'payment_url': 'https://test.payu.in/_payment',
    }
}
```


Run migration: use `python manage.py migrate`.


Add following to the dashboard navigation:

```python
OSCAR_DASHBOARD_NAVIGATION += [{
    'label': _('Payments'),
    'icon': 'icon-globe',
    'children': [
        {
            'label': _('Paypal Express transactions'),
            'url_name': 'paypal-express-list',
        },
        {
            'label': _('Payu transactions'),
            'url_name': 'payu-nonseamless-list',
        },
        {
            'label': _('COD Transaction Lists'),
            'url_name': 'cashondelivery-transaction-list',
        },
    ]
}]
```


Add PayU urls to `url.py` file:

```python
from payu.nonseamless.dashboard.app import application as payu

urlpatterns = [
    url(r'^checkout/payu/', include('payu.nonseamless.urls')),
    url(r'^dashboard/payu/', include(payu.urls)),
]
```

