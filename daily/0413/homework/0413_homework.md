# 0413_homework

### 아래 코드들을 참고하여 각 문항에 답하시오.

1. django에서 기본적으로 사용하는 User 모델은 다음과 같은 경로에서 찾아볼 수 있다.

   ```python
   from django.contrib.auth.models import User
   ```

   - 아래의 Django 공식 저장소에서 User 모델이 정의된 코드를 찾아 작성하시오.
     https://github.com/django/django

   > ```python
   > class User(AbstractUser):
   >     """
   >     Users within the Django authentication system are represented by this
   >     model.
   >     Username and password are required. Other fields are optional.
   >     """
   >     class Meta(AbstractUser.Meta):
   >         swappable = 'AUTH_USER_MODEL'
   > ```
   >
   > ```python
   > class AbstractUser(AbstractBaseUser, PermissionsMixin):
   >     """
   >     An abstract base class implementing a fully featured User model with
   >     admin-compliant permissions.
   >     Username and password are required. Other fields are optional.
   >     """
   >     username_validator = UnicodeUsernameValidator()
   > 
   >     username = models.CharField(
   >         _('username'),
   >         max_length=150,
   >         unique=True,
   >         help_text=_('Required. 150 characters or fewer. Letters, digits and @/./+/-/_ only.'),
   >         validators=[username_validator],
   >         error_messages={
   >             'unique': _("A user with that username already exists."),
   >         },
   >     )
   >     first_name = models.CharField(_('first name'), max_length=150, blank=True)
   >     last_name = models.CharField(_('last name'), max_length=150, blank=True)
   >     email = models.EmailField(_('email address'), blank=True)
   >     is_staff = models.BooleanField(
   >         _('staff status'),
   >         default=False,
   >         help_text=_('Designates whether the user can log into this admin site.'),
   >     )
   >     is_active = models.BooleanField(
   >         _('active'),
   >         default=True,
   >         help_text=_(
   >             'Designates whether this user should be treated as active. '
   >             'Unselect this instead of deleting accounts.'
   >         ),
   >     )
   >     date_joined = models.DateTimeField(_('date joined'), default=timezone.now)
   > 
   >     objects = UserManager()
   > 
   >     EMAIL_FIELD = 'email'
   >     USERNAME_FIELD = 'username'
   >     REQUIRED_FIELDS = ['email']
   > 
   >     class Meta:
   >         verbose_name = _('user')
   >         verbose_name_plural = _('users')
   >         abstract = True
   > 
   >     def clean(self):
   >         super().clean()
   >         self.email = self.__class__.objects.normalize_email(self.email)
   > 
   >     def get_full_name(self):
   >         """
   >         Return the first_name plus the last_name, with a space in between.
   >         """
   >         full_name = '%s %s' % (self.first_name, self.last_name)
   >         return full_name.strip()
   > 
   >     def get_short_name(self):
   >         """Return the short name for the user."""
   >         return self.first_name
   > 
   >     def email_user(self, subject, message, from_email=None, **kwargs):
   >         """Send an email to this user."""
   >         send_mail(subject, message, from_email, [self.email], **kwargs)
   > ```
   >
   > ```python
   > class AbstractBaseUser(models.Model):
   >     password = models.CharField(_('password'), max_length=128)
   >     last_login = models.DateTimeField(_('last login'), blank=True, null=True)
   > 
   >     is_active = True
   > 
   >     REQUIRED_FIELDS = []
   > 
   >     # Stores the raw password if set_password() is called so that it can
   >     # be passed to password_changed() after the model is saved.
   >     _password = None
   > 
   >     class Meta:
   >         abstract = True
   > 
   >     def __str__(self):
   >         return self.get_username()
   > 
   >     def save(self, *args, **kwargs):
   >         super().save(*args, **kwargs)
   >         if self._password is not None:
   >             password_validation.password_changed(self._password, self)
   >             self._password = None
   > 
   >     def get_username(self):
   >         """Return the username for this User."""
   >         return getattr(self, self.USERNAME_FIELD)
   > 
   >     def clean(self):
   >         setattr(self, self.USERNAME_FIELD, self.normalize_username(self.get_username()))
   > 
   >     def natural_key(self):
   >         return (self.get_username(),)
   > 
   >     @property
   >     def is_anonymous(self):
   >         """
   >         Always return False. This is a way of comparing User objects to
   >         anonymous users.
   >         """
   >         return False
   > 
   >     @property
   >     def is_authenticated(self):
   >         """
   >         Always return True. This is a way to tell if the user has been
   >         authenticated in templates.
   >         """
   >         return True
   > 
   >     def set_password(self, raw_password):
   >         self.password = make_password(raw_password)
   >         self._password = raw_password
   > 
   >     def check_password(self, raw_password):
   >         """
   >         Return a boolean of whether the raw_password was correct. Handles
   >         hashing formats behind the scenes.
   >         """
   >         def setter(raw_password):
   >             self.set_password(raw_password)
   >             # Password hash upgrades shouldn't be considered password changes.
   >             self._password = None
   >             self.save(update_fields=["password"])
   >         return check_password(raw_password, self.password, setter)
   > 
   >     def set_unusable_password(self):
   >         # Set a value that will never be a valid hash
   >         self.password = make_password(None)
   > 
   >     def has_usable_password(self):
   >         """
   >         Return False if set_unusable_password() has been called for this user.
   >         """
   >         return is_password_usable(self.password)
   > 
   >     def get_session_auth_hash(self):
   >         """
   >         Return an HMAC of the password field.
   >         """
   >         key_salt = "django.contrib.auth.models.AbstractBaseUser.get_session_auth_hash"
   >         return salted_hmac(key_salt, self.password).hexdigest()
   > 
   >     @classmethod
   >     def get_email_field_name(cls):
   >         try:
   >             return cls.EMAIL_FIELD
   >         except AttributeError:
   >             return 'email'
   > 
   >     @classmethod
   >     def normalize_username(cls, username):
   >         return unicodedata.normalize('NFKC', username) if isinstance(username, str) else username
   > ```

2. 기본 User 모델의 정보를 생성하기 위하여 Django 내부에 정의된 ModelForm을 불러오는 import 문장을 작성하시오.

   ```python
   from django.contrib.auth.forms import UserCreationForm
   ```

3. views.py에 정의된 함수를 POST 요청에 대해서만 실행하게 하기 위하여 추가하는 require_POST 함수를 불러오는 import 문장을 작성하시오.

   ```python
   from django.views.decorators.http import require_POST
   ```