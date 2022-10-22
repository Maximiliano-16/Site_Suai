## Site_Suai
____
## Цель работы:
Спроектировать и разработать систему авторизации пользователей на протокоде HTTP
## Реализованные возможности
+ функциональность входа/выхода
+ хранение паролей в хешированном виде
+ форма регистрации
+ смена пароля
+ восстановление пароля
+ ограниичение времени сессии
+ валидация пароля
+ хранение хеша пароля с солью
____
## Ход работы
### 1. Разработка пользовательского интерфейса
В ходе выполнения работы был разработан пользовательский интерфейс при помощи графического редактора [Figma](https://www.figma.com/community)

+ Интерфейс главной страници для неавторизованных пользователей и страница авторизации

![figma1](https://user-images.githubusercontent.com/98755619/197325213-f7bfa644-b26f-4726-a218-2e9ceb341bfb.png)
----
+ Интерфейс страницы регистрации и страницы сброса пароля

![figma2](https://user-images.githubusercontent.com/98755619/197325224-510c3fa4-1182-4231-a11f-0868f5b3cd14.png)
----
+ Интерфейс главной страницы для авторизированных пользователей и страницы смены пароля
 
![figma3](https://user-images.githubusercontent.com/98755619/197325258-312f5316-a61e-47c8-b99d-0395ea0a6b93.png)

### 2. Описание пользовательских сценариев работы
+ #### Сценарий регистрации
1) Пользователь заходит на сайт и попадает на главную страничку, на которой нажимает кнопку "Зарегистрироваться",
после этого клиента перекидывает на страничку регистрации.
2) Клиент должен заполнить все поля и при успешном заполнении отправить форму, в противном случае будет выпадать ошибка
регистрации с указанием проблемы.
3) После этого пользователя перекинет на основную страничку сайта.
+ #### Сценарий входа
1) Пользователь заходит на сайт и попадает на главную страничку, Если пользователь уже зарегистрирован на сайте,
то он может нажать на кнопку "Войти", после этого клиента перекидывает на страничку входа.
2) Клиент должен заполнить поля данными, которые он указывал при регистрации, и при успешном заполнении отправить форму,
в противном случае будет выпадать ошибка входа.
3) После успешного входа пользователя перекинет на основную страничку сайта.
+ #### Сценарий восстановления пароля
1) Пользователь заходит на сайт и попадает на главную страничку, если пользователь уже зарегистрирован на сайте,
но забыл пароль, то он может нажать на кнопку "Забыли пароль?", после этого клиента перекидывает на страничку
восстановления пароля.
2) Клиент должен указать адрес электронной почты, который он указывал при регистрации, после этого ему на почту придёт
письмо с дальнейшими инструкциями
3) Пользователь должен открыть письмо и перейти по ссылке в нём, после этого его перекинет на страничку ввода
нового пароля
4) После заполнения полей по смене пароля пользователь сможет зайти на сайт по новому паролю
+ #### Сценарий смены пароля
1) Пользователь заходит на сайт и попадает на главную страничку, после этого заходит в свой аккаунт.
2) Если Пользователь хочет сменить пароль, то ему требуется нажать на кнопку "Сменить пароль?", после этого клиента
перекидывает на страничку изменения пароля.
3) Клиент должен заполнить поля связанные со старым и новым паролями, затем при успешном заполнении отправить форму,
в противном случае будет выпадать ошибка смены пароля.
4) После этого пользователь сможет заходить в свой аккаунт под новым паролем.
### 3. Описание API сервера и хореографии

+ Пример запросов, когда пользователь проходит процесс регистрации на сайте

![SignUp](https://user-images.githubusercontent.com/98755619/197325433-e49c679b-2351-4b45-afc7-232e84fa79a4.png)
----
+ Пример запросов, когда пользователь проходит процесс авторизации на сайте

![login](https://user-images.githubusercontent.com/98755619/197325502-30deff0e-77b4-40ae-ab5d-66da2cf0031d.png)
----
+ Пример запросов, когда пользователь проходит процесс сброса пароля на сайте

![PasswordReset](https://user-images.githubusercontent.com/98755619/197325534-9706cdce-40e6-4ea0-a173-ce4d92e7d65e.png)
----
+ Пример запросов, когда пользователь проходит процесс смены пароля на сайте

![PasswordChange](https://user-images.githubusercontent.com/98755619/197325553-df61ed4b-6b57-4d97-85ab-f597cad1febd.png)

### 4. Описание структура базы данных

Для хранения данных использовалась встраиваемая кроссплатформенная БД - SQLite

Пример хранения данных пользователя Max:

| id           | password                               | last_login                 | username | first_name | email       | is_active | date_joined                |
|--------------|----------------------------------------|----------------------------|----------|------------|-------------|-----------|----------------------------|
| 1            | pbkdf2_sha256$15..0$3..D$op1..p7/Wh..Q | 2022-10-17 16:47:26.099217 | Max      | Maxim      | Max@mail.ru | 1         | 2022-10-04 18:19:32.425677 |

### 5. Описание алгоритмов 
+ Алгоритм действий пользователя при регистрации на сайте

![SignUp_block drawio](https://user-images.githubusercontent.com/98755619/197325617-2afea13d-ddcd-4fe7-b16a-30d4859d739a.png)
----

+ Алгоритм действий пользователя про авторизации на сайте

![login drawio](https://user-images.githubusercontent.com/98755619/197325649-d07eb42b-16d9-4ae7-8e8a-8d244a5dfc80.png)

### 6. Значимые фрагменты кода

Код модели User:
```sh
class AbstractUser(AbstractBaseUser, PermissionsMixin):
    """
    An abstract base class implementing a fully featured User model with
    admin-compliant permissions.

    Username and password are required. Other fields are optional.
    """
    username_validator = UnicodeUsernameValidator()

    username = models.CharField(
        _('username'),
        max_length=150,
        unique=True,
        help_text=_('Required. 150 characters or fewer. Letters, digits and @/./+/-/_ only.'),
        validators=[username_validator],
        error_messages={
            'unique': _("A user with that username already exists."),
        },
    )
    first_name = models.CharField(_('first name'), max_length=30, blank=True)
    last_name = models.CharField(_('last name'), max_length=150, blank=True)
    email = models.EmailField(_('email address'), blank=True)
    is_staff = models.BooleanField(
        _('staff status'),
        default=False,
        help_text=_('Designates whether the user can log into this admin site.'),
    )
    is_active = models.BooleanField(
        _('active'),
        default=True,
        help_text=_(
            'Designates whether this user should be treated as active. '
            'Unselect this instead of deleting accounts.'
        ),
    )
    date_joined = models.DateTimeField(_('date joined'), default=timezone.now)

    objects = UserManager()

    EMAIL_FIELD = 'email'
    USERNAME_FIELD = 'username'
    REQUIRED_FIELDS = ['email']

    class Meta:
        verbose_name = _('user')
        verbose_name_plural = _('users')
        abstract = True

    def clean(self):
        super().clean()
        self.email = self.__class__.objects.normalize_email(self.email)

    def get_full_name(self):
        """
        Return the first_name plus the last_name, with a space in between.
        """
        full_name = '%s %s' % (self.first_name, self.last_name)
        return full_name.strip()

    def get_short_name(self):
        """Return the short name for the user."""
        return self.first_name

    def email_user(self, subject, message, from_email=None, **kwargs):
        """Send an email to this user."""
        send_mail(subject, message, from_email, [self.email], **kwargs)
```

Процесс создания сессии при авторизации:
```sh
def login(request, user, backend=None):
    """
    Persist a user id and a backend in the request. This way a user doesn't
    have to reauthenticate on every request. Note that data set during
    the anonymous session is retained when the user logs in.
    """
    session_auth_hash = ''
    if user is None:
        user = request.user
    if hasattr(user, 'get_session_auth_hash'):
        session_auth_hash = user.get_session_auth_hash()

    if SESSION_KEY in request.session:
        if _get_user_session_key(request) != user.pk or (
                session_auth_hash and
                not constant_time_compare(request.session.get(HASH_SESSION_KEY, ''), session_auth_hash)):
            # To avoid reusing another user's session, create a new, empty
            # session if the existing session corresponds to a different
            # authenticated user.
            request.session.flush()
    else:
        request.session.cycle_key()

    try:
        backend = backend or user.backend
    except AttributeError:
        backends = _get_backends(return_tuples=True)
        if len(backends) == 1:
            _, backend = backends[0]
        else:
            raise ValueError(
                'You have multiple authentication backends configured and '
                'therefore must provide the `backend` argument or set the '
                '`backend` attribute on the user.'
            )
    else:
        if not isinstance(backend, str):
            raise TypeError('backend must be a dotted import path string (got %r).' % backend)

    request.session[SESSION_KEY] = user._meta.pk.value_to_string(user)
    request.session[BACKEND_SESSION_KEY] = backend
    request.session[HASH_SESSION_KEY] = session_auth_hash
    if hasattr(request, 'user'):
        request.user = user
    rotate_token(request)
    user_logged_in.send(sender=user.__class__, request=request, user=user)
```

![как хранятся пароли](https://user-images.githubusercontent.com/98755619/197329672-32ec84a1-5864-42fb-9e6f-97f7d8227e37.png)

Основные используемые библиотеки

![используемые библиотеки](https://user-images.githubusercontent.com/98755619/197329700-79aae348-5678-43da-a3ff-cba350bd6d36.png)

Реализция сессий

![сессии1](https://user-images.githubusercontent.com/98755619/197329769-b7fb1210-32db-4c4f-a018-97b76702d268.png)
![сессии2](https://user-images.githubusercontent.com/98755619/197329776-88b1df92-1afb-4170-9cfa-e0b7767c727c.png)
![сессии3](https://user-images.githubusercontent.com/98755619/197329790-d3589fd2-c5b6-45af-997a-95d0f5dfdfe3.png)

