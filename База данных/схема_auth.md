# Схема auth
## Оглавление 

1 [Таблица пользователь](#таблица-user-пользователь)

2 [Таблица токен](#таблица-token-токен)

3 [Таблица права](#таблица-right-права)

4 [Таблица ролей](#таблица-roles-роли)

5 [Таблица право ролей](#таблица-right_roles-право-ролей)

6 [Таблица роли пользователей](#таблица-roles_user-роли-пользователей)

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