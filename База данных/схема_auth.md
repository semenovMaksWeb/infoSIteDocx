# Схема auth

схема реализующая в себе весь функционал связанный с пользователем:

- crud с пользователем
- crud с правами
- crud с ролями 
- crud с токенами
- crud с правами, ролями, токенами пользователей
- crud настройками пользователей

## таблица user (пользователь)
| Имя поля | Тип поля | PK | unique | FK | default |
| - | - | - | - | - | - |
| id | int | - | - | - | - |
| name | varchar(64) | - | - | - | - |
| surname | varchar(64) | - | - | - | - |
| middlename | varchar(64) | - | - | - | - |
| email | varchar(128) | - | + | - | - |
| password | text | - | - | - | - |
| is_active | bool | - | - | - | true |
| is_email | bool | - | - | - | false |

## таблица token (токен)
| Имя поля | Тип поля | PK | unique | FK | default |
| - | - | - | - | - | - |
| id | int | - | - | - | - |
| access_token | varchar(128) | - | + | - | - |
| refresh_token | varchar(128) | - | + | - | - |
| is_active | bool | - | - | - | true |
| date_create | datetime | - | - | - | now() |
| time_life | datetime | - | - | - | now() + 30 min |
