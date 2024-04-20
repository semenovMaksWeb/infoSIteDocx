# Схема auth
## Оглавление 

1 [Таблица пользователь](#таблица-user-пользователь)

2 [Таблица токен](#таблица-token-токен)

3 [Таблица права](#таблица-right-права)

4 [Таблица ролей](#таблица-roles-роли)

5 [Таблица право ролей](#таблица-right_roles-право-ролей)

6 [Таблица роли пользователей](#таблица-roles_user-роли-пользователей)

7 [Функции auth](#функции-схемы-auth)

схема реализующая в себе весь функционал связанный с пользователем:
- crud с пользователем
- crud с токенами
- crud с правами
- crud с ролями 
- crud с правами, ролями
- crud настройками пользователей

## таблица user (пользователь)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| name | varchar(64) | - | - | - | - | + |
| surname | varchar(64) | - | - | - | - | + |
| middlename | varchar(64) | - | - | - | - | - |
| email | varchar(128) | - | + | - | - | + |
| password | varchar(60) | - | - | - | - | + |
| is_active | bool | - | - | - | true | + |
| is_email | bool | - | - | - | false | + |

## таблица token (токен)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| access_token | varchar(128) | - | + | - | - | + |
| refresh_token | varchar(128) | - | + | - | - | + |
| is_active | bool | - | - | - | true | + |
| date_create | datetime | - | - | - | now() | + |
| time_life | datetime | - | - | - | now() + 30 min | + |
| id_user | int | - | - | user | - | + |

## таблица right (права)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| const_name | varchar(128) | - | + | - | - | + |
| name | varchar(128) | - | + | - | - | + |
| description | varchar(128) | - | - | - | - | + |
| is_active | bool | - | - | - | true | + |

## таблица roles (роли)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| const_name | varchar(128) | - | + | - | - | + |
| name | varchar(128) | - | + | - | - | + |
| description | varchar(128) | - | - | - | - | + |
| is_active | bool | - | - | - | true | + |

## таблица right_roles (право ролей)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| id_roles | int | - | - | roles | - | + |
| id_right | int | - | - | right | - | + |

Дополнительная информация: 
ограничения UNIQUE (id_roles, id_right)

## таблица roles_user (роли пользователей)
| Имя поля | Тип поля | PK | unique | FK | default | Not null
| - | - | - | - | - | - | - |
| id | int | - | - | - | - | - |
| id_roles | int | - | - | roles | - | + |
| id_user | int | - | - | user | - | + |

Дополнительная информация: 
ограничения UNIQUE (id_roles, id_user)

## Функции схемы auth:
- **Пользовательские функции**:
    - <input type="checkbox" checked> **auth.register** - функция по регистрации пользователя
    - <input type="checkbox">**auth.authorization** - функция по авторизации пользователя
    - <input type="checkbox">**auth.authentication** - функция по аутентификации пользователя
    - <input type="checkbox" checked>**auth.exit** - функция выхода пользователя из системы текущей сессий
    - <input type="checkbox" checked>**auth.exit_all** - функция выхода всех токенов из системы кроме текущей сессий (для конкретного пользователя)
    - <input type="checkbox">**auth.verification_email** - функция подвержает электронную почту клиента
    - <input type="checkbox">**auth.get_profile** - функция возвращает данные о конкретном пользователи (по токену)
    - <input type="checkbox">**auth.user_update** - функция меняющая данные о пользователе
- **Технические функции**:
    - <input type="checkbox">**auth.token_get** - функция возвращает токен по его (access_token)
    - <input type="checkbox"> **auth.token_update** - функция изменяющая токен 
    - <input type="checkbox" checked> **auth.token_create** - функция создание токена
    - **auth.user_get** - функция возвращает пользователя, его право и роли (по токену или id) #TODO
    - <input type="checkbox" checked> **auth.token_delete_user_id** - функция удаляющая все токены для конкретного пользователя(или группы пользователей)
    - <input type="checkbox" checked> **auth.user_check_validate** - функция проверять валидацию создание или изменения пользователя
    - <input type="checkbox" checked> **auth.user_check_id** - функция проверять наличия пользователя по id
    - <input type="checkbox" checked> **auth.user_check_authorization** - функция проверять наличия пользователя по логину и паролю
- **Админские функции**:
    - <input type="checkbox" checked> **auth.banned_user** - функция блокирует конкретного пользователя
    - <input type="checkbox" checked> **auth.unblock_user** - функция разблокирует конкретного пользователя
    - <input type="checkbox">**auth.user_get_list** - функция возвращаюся список пользователей
    - <input type="checkbox">**auth.token_get_list** - функция возвращаюся список токенов
    - <input type="checkbox">**auth.right_get_list** - функция возвращаюся список прав
    - <input type="checkbox">**auth.roles_get_list** - функция возвращаюся список ролей
    - <input type="checkbox">**auth.rights_this_role_get_list** - функция возвращаюся список прав для конкретной роли (или список прав которых нет у роли)
    - <input type="checkbox"> **auth.roles_this_right_get_list** - функция возвращаюся список ролей где есть конкретной право (или список ролей у которых нет у право)
    - <input type="checkbox"> **auth.user_create** - функция создает пользователя
    - <input type="checkbox"> **auth.right_create** - функция создает право
    - <input type="checkbox"> **auth.role_create** - функция создает роль
    - <input type="checkbox"> **auth.user_update** - функция изменить пользователя
    - <input type="checkbox"> **auth.right_update** - функция изменить право
    - <input type="checkbox"> **auth.role_update** - функция изменить роль
    - <input type="checkbox"> **auth.right_roles_update_list** - функция (добавляет, удаляет) права для конкретной роли
    - <input type="checkbox"> **auth.roles_user_update_list** - функция (добавляет, удаляет) роли для конкретной пользователя
    - <input type="checkbox"> **auth.token_delete** - функции удаляет токены по ids