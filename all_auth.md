## Install
```py
pip install django-allauth
```

# Add Some Configartions in setting.py

```py
# after database conf
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend',
]

LOGIN_REDIRECT_URL = "/"
LOGOUT_REDIRECT_URL = "/"
```

```py 
# add in APPs
    # All AUth
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google', #which we need like facebook/github /apple or more
```

```py
# after apps 
SITE_ID = 2

SOCIALACCOUNT_PROVIDERS = {
    'google': {

        'APP': {
            'client_id': '123',
            'secret': '123',
            'key': ''
        }
    }
}

```

```py
# add path in urls
 path('accounts/', include('allauth.urls')),
#  logout login and forgatepassword all functionality give this modul
```

- migrate our tables

- find our login page

```py
http://127.0.0.1:8000/accounts/login/
```

- create superuser and go to admin pannel

## Google Gmail Enable API 
link :https://console.cloud.google.com/apis/credentials/consent/edit;newAppInternalUser=false?project=jarvish-1bf8c
- create our api for all auth 

## My Data
```py
"client_id":"600677695055-af3m1nc371f7oq9dmd839gs86255oopr.apps.googleusercontent.com"
"project_id":"jarvish-1bf8c"
"auth_uri":"https://accounts.google.com/o/oauth2/auth"
"token_uri":"https://oauth2.googleapis.com/token"
"auth_provider_x509_cert_url":"https://www.googleapis.com/oauth2/v1/certs"
"client_secret":"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",
"redirect_uris":"http://127.0.0.1:8000"
```


```py
Home › Social Accounts › Social applications › Add social application
- Add some Details and Submit
```


# Custom Auth Page

setting.py
```py
ACCOUNT_LOGIN_TEMPLATE = 'account/login.html'
```
```py
# file Structure 
Template 
├── account/
│   ├── base.html
│   ├── _messages.html
│   ├── login.html
│   ├── logout.html
│   ├── password_change.html
│   ├── password_reset.html
│   ├── signup.html
│   ├── email/
│   │   ├── change.html
│   │   ├── confirm_email_message.txt
│   │   └── signup_message.txt

- chnage all setting like base template and all and manupilate as we need 
```

### NOtes:

    EMAIL_FIELD = "email"
    REQUIRED_FIELDS = ["email"]

- Remove username and user Email Field as a required fields and  migrate again the tables 
