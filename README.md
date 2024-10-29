<p align="center">
  <a href="https://www.django-rest-framework.org/"><img width="420px" src="https://raw.githubusercontent.com/encode/django-rest-framework/refs/heads/master/docs/img/logo.png" alt='rest_framework'></a>
</p>
<p align="center">
    <em>Web APIs for Django. 🎸</em>
</p>

---

[![build-status-image]][build-status]
[![coverage-status-image]][codecov]
[![pypi-version]][pypi]

[build-status-image]: https://github.com/encode/django-rest-framework/actions/workflows/main.yml/badge.svg
[build-status]: https://github.com/encode/django-rest-framework/actions/workflows/main.yml
[coverage-status-image]: https://img.shields.io/codecov/c/github/encode/django-rest-framework/master.svg
[codecov]: https://codecov.io/github/encode/django-rest-framework?branch=master
[pypi-version]: https://img.shields.io/pypi/v/djangorestframework.svg
[pypi]: https://pypi.org/project/djangorestframework/

---

**Documentation**: [https://www.django-rest-framework.org][docs]

**Source Code**: [https://github.com/encode/django-rest-framework][source]

---

# Django REST framework

Django REST framework is a powerful and flexible toolkit for building Web APIs.

Some reasons you might want to use REST framework:

* The Web browsable API is a huge usability win for your developers.
* [Authentication policies][authentication] including optional packages for [OAuth1a][oauth1-section]
  and [OAuth2][oauth2-section].
* [Serialization][serializers] that supports both [ORM][modelserializer-section] and [non-ORM][serializer-section] data
  sources.
* Customizable all the way down - just use [regular function-based views][functionview-section] if you don't need
  the [more][generic-views] [powerful][viewsets] [features][routers].
* [Extensive documentation][docs], and [great community support][group].

[oauth1-section]: https://www.django-rest-framework.org/api-guide/authentication/#django-rest-framework-oauth
[oauth2-section]: https://www.django-rest-framework.org/api-guide/authentication/#django-oauth-toolkit
[serializer-section]: https://www.django-rest-framework.org/api-guide/serializers/#serializers
[modelserializer-section]: https://www.django-rest-framework.org/api-guide/serializers/#modelserializer
[functionview-section]: https://www.django-rest-framework.org/api-guide/views/#function-based-views
[generic-views]: https://www.django-rest-framework.org/api-guide/generic-views/
[viewsets]: https://www.django-rest-framework.org/api-guide/viewsets/
[routers]: https://www.django-rest-framework.org/api-guide/routers/
[serializers]: https://www.django-rest-framework.org/api-guide/serializers/
[authentication]: https://www.django-rest-framework.org/api-guide/authentication/]()

**Below**: *Screenshot from the browsable API*

![Screenshot][image]

---

## Funding

REST framework is a *collaboratively funded project*. If you use
REST framework commercially we strongly encourage you to invest in its
continued development by [signing up for a paid plan][funding].

The initial aim is to provide a single full-time position on REST framework.
*Every single sign-up makes a significant impact towards making that possible.*

[![][sentry-img]][sentry-url]
[![][stream-img]][stream-url]
[![][spacinov-img]][spacinov-url]
[![][retool-img]][retool-url]
[![][bitio-img]][bitio-url]
[![][posthog-img]][posthog-url]
[![][cryptapi-img]][cryptapi-url]
[![][fezto-img]][fezto-url]
[![][svix-img]][svix-url]
[![][zuplo-img]][zuplo-url]

[funding]: https://fund.django-rest-framework.org/topics/funding/
[sponsors]: https://fund.django-rest-framework.org/topics/funding/#our-sponsors

[sentry-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/sentry-readme.png
[sentry-url]: https://getsentry.com/welcome/

[stream-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/stream-readme.png
[stream-url]: https://getstream.io/?utm_source=DjangoRESTFramework&utm_medium=Webpage_Logo_Ad&utm_content=Developer&utm_campaign=DjangoRESTFramework_Jan2022_HomePage

[spacinov-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/spacinov-readme.png
[spacinov-url]: https://www.spacinov.com/

[retool-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/retool-readme.png
[retool-url]: https://retool.com/?utm_source=djangorest&utm_medium=sponsorship

[bitio-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/bitio-readme.png
[bitio-url]: https://bit.io/jobs?utm_source=DRF&utm_medium=sponsor&utm_campaign=DRF_sponsorship

[posthog-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/posthog-readme.png
[posthog-url]: https://posthog.com?utm_source=drf&utm_medium=sponsorship&utm_campaign=open-source-sponsorship

[cryptapi-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/cryptapi-readme.png
[cryptapi-url]: https://cryptapi.io

[fezto-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/fezto-readme.png
[fezto-url]: https://www.fezto.xyz/?utm_source=DjangoRESTFramework

[svix-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/svix-premium.png
[svix-url]: https://www.svix.com/?utm_source=django-REST&utm_medium=sponsorship

[zuplo-img]: https://raw.githubusercontent.com/encode/django-rest-framework/master/docs/img/premium/zuplo-readme.png
[zuplo-url]: https://zuplo.link/django-gh

---

## Requirements

* Python 3.8+
* Django 4.2, 5.0, 5.1

We **highly recommend** and only officially support the latest patch release of
each Python and Django series.

---

## Installation

Install using `pip`...

```bash
pip install djangorestframework
```

Add `'rest_framework'` to your `INSTALLED_APPS` setting.

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

---

## Example

Let's take a look at a quick example of using REST framework to build a simple model-backed API for accessing users and
groups.

Startup up a new project like so...

    pip install django
    pip install djangorestframework
    django-admin startproject example .
    ./manage.py migrate
    ./manage.py createsuperuser

Now edit the `example/urls.py` module in your project:

```python
from django.contrib.auth.models import User
from django.urls import include, path
from rest_framework import routers, serializers, viewsets


# Serializers define the API representation.
class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ['url', 'username', 'email', 'is_staff']


# ViewSets define the view behavior.
class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer


# Routers provide a way of automatically determining the URL conf.
router = routers.DefaultRouter()
router.register(r'users', UserViewSet)

# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    path('', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework')),
]
```

We'd also like to configure a couple of settings for our API.

Add the following to your `settings.py` module:

```python
INSTALLED_APPS = [
    ...  # Make sure to include the default installed apps here.
    'rest_framework',
]

REST_FRAMEWORK = {
    # Use Django's standard `django.contrib.auth` permissions,
    # or allow read-only access for unauthenticated users.
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly',
    ]
}
```

That's it, we're done!

```shell
./manage.py runserver
```

You can now open the API in your browser at `http://127.0.0.1:8000/`, and view your new 'users' API. If you use the
`Login` control in the top right corner you'll also be able to add, create and delete users from the system.

You can also interact with the API using command line tools such as [`curl`](https://curl.haxx.se/). For example, to
list the users endpoint:

```shell
$ curl -H 'Accept: application/json; indent=4' -u admin:password http://127.0.0.1:8000/users/
    [
        {
            "url": "http://127.0.0.1:8000/users/1/",
            "username": "admin",
            "email": "admin@example.com",
            "is_staff": true,
        }
    ]
```

Or to create a new user:

```shell
$ curl -X POST -d username=new -d email=new@example.com -d is_staff=false -H 'Accept: application/json; indent=4' -u admin:password http://127.0.0.1:8000/users/
    {
        "url": "http://127.0.0.1:8000/users/2/",
        "username": "new",
        "email": "new@example.com",
        "is_staff": false,
    }
```

---

## Documentation & Support

Full documentation for the project is available at [https://www.django-rest-framework.org/][docs].

For questions and support, use the [REST framework discussion group][group], or `#restframework` on libera.chat IRC.

---

## Security

Please see the [security policy][security-policy].

[security-policy]: https://github.com/encode/django-rest-framework/security/policy

---

<p align="center">
<i>Django REST framework is licensed under the
<a href="https://github.com/encode/django-rest-framework/blob/master/LICENSE.md">BSD 3-Clause "New" or "Revised"</a> License.<br/>
Designed & crafted with care.</i><br/>
&mdash; 🎸 &mdash;
</p>


<!-- Common links -->
[group]: https://groups.google.com/forum/?fromgroups#!forum/django-rest-framework
[image]: https://www.django-rest-framework.org/img/quickstart.png
[docs]: https://www.django-rest-framework.org/
[source]: https://github.com/encode/django-rest-framework
[license]: https://github.com/encode/django-rest-framework/blob/master/LICENSE.md
