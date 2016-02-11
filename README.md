#CUser

CUser makes it easy to use email address as your identification token instead of a username.

CUser is a custom Django User model (extends AbstractBaseUser) so it takes a tiny amount of effort to use.

The only difference between CUser and the vanilla Django User is email address is the `USERNAME_FIELD` (and username does not exist).

**Why use CUser?** Because you still want everything in `django.contrib.auth`, but you also want to log in user's with their email addresses.

##Install & Set up

0. If you previously used Django's default User model (`django.contrib.auth.User`), jump to **Notes**. Otherwise, continue onward!

1. Add "cuser" to your INSTALLED_APPS setting like this
    
        INSTALLED_APPS = [
            ...
            'cuser',
        ]

2. Specify the custom model as the default user model for your project using the AUTH_USER_MODEL setting in your settings.py:
   
    AUTH_USER_MODEL = 'cuser.CUser'

3. Run `python manage.py migrate` to create CUser's models.

4. Instead of referring to User directly, you should reference the user model using `django.contrib.auth.get_user_model()`

## Notes

If you have tables referencing Django's User model, you will have to delete those table and migrations, then re-migrate. This will ensure everything is set up correctly from the beginning.

When you define a foreign key or many-to-many relations to the User model, you should specify the custom model using the `AUTH_USER_MODEL` setting.

For example:
    
    from django.conf import settings
    from django.db import models

    class Profile(models.Model):
        user = models.ForeignKey(
            settings.AUTH_USER_MODEL,
            on_delete=models.CASCADE,
    )

##Questions, comments, or anything else?

* [Submit an issue](https://github.com/thomasmeagher/django-email-username/issues/new "Submit and issue")
* [Twitter](https://twitter.com/thomasmeagher "@thomasmeagher")
* tom@meagher.co