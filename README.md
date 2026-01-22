# Домашнее задание к занятию "`Базы данных`" - `Яковлева Александра`

# Задание 1
Опишите не менее семи таблиц, из которых состоит база данных. Определите:

какие данные хранятся в этих таблицах,
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Начертите схему полученной модели данных. Можете использовать онлайн-редактор: https://app.diagrams.net/

Этапы реализации:

Внимательно изучите предоставленный вам файл с данными и подумайте, как можно сгруппировать данные по смыслу.
Разбейте исходный файл на несколько таблиц и определите список столбцов в каждой из них.
Для каждого столбца подберите подходящий тип данных из PostgreSQL.
Для каждой таблицы определите первичный ключ (PRIMARY KEY).
Определите типы связей между таблицами.
Начертите схему модели данных. На схеме должны быть чётко отображены:
все таблицы с их названиями,
все столбцы с указанием типов данных,
первичные ключи (они должны быть явно выделены),
линии, показывающие связи между таблицами.
Результатом выполнения задания должен стать скриншот получившейся схемы базы данных.

Этапы реализации:
Внимательно изучите предоставленный вам файл с данными и подумайте, как можно сгруппировать данные по смыслу.
Разбейте исходный файл на несколько таблиц и определите список столбцов в каждой из них.
Для каждого столбца подберите подходящий тип данных из PostgreSQL.
Для каждой таблицы определите первичный ключ (PRIMARY KEY).
Определите типы связей между таблицами.
Начертите схему модели данных. На схеме должны быть чётко отображены: все таблицы с их названиями, все столбцы с указанием типов данных, первичные ключи (они должны быть явно выделены), линии, показывающие связи между таблицами.
Результатом выполнения задания должен стать скриншот получившейся схемы базы данных.
ОТВЕТ:
Таблицы:

Employees (Сотрудники) id (PK) — уникальный идентификатор last_name — Фамилия (50) first_name — Имя (50) patronymic — Отчество (50) position_id (FK) → Positions(id) department_id (FK) → Departments(id) hire_date — дата принятия на работу salary — оклад (DECIMAL)
Код:

CREATE TABLE Employees (
    id SERIAL PRIMARY KEY,
    last_name VARCHAR(50) NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    patronymic VARCHAR(05),
    position_id INTEGER REFERENCES Positions(id),
    department_id INTEGER REFERENCES Departments(id),
    hire_date DATE NOT NULL,
    salary DECIMAL(10,2) NOT NULL CHECK (salary > 0)
);
Positions (Должности) id (PK) title — название должности
Код:

CREATE TABLE Positions (
    id SERIAL PRIMARY KEY,
    title VARCHAR(150) NOT NULL UNIQUE
);
Departments (Подразделения) id (PK) name — название подразделения type_id (FK) → DepartmentTypes(id) branch_id (FK) → Branches(id)
Код:

CREATE TABLE Departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    type_id INTEGER REFERENCES DepartmentTypes(id),
    branch_id INTEGER REFERENCES Branches(id)
);
DepartmentTypes (Типы подразделений) id (PK) name — название типа
Код:

CREATE TABLE DepartmentTypes (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);
Branches (Филиалы) id (PK) address — адрес филиала
Код:

CREATE TABLE Branches (
    id SERIAL PRIMARY KEY,
    address TEXT NOT NULL
);
Projects (Проекты) id (PK) name — название проекта
Код:

CREATE TABLE Projects (
    id SERIAL PRIMARY KEY,
    name VARCHAR(200) NOT NULL UNIQUE
);
ProjectAssignments (Назначения на проекты) employee_id (FK) → Employees(id) project_id (FK) → Projects(id) assignment_date — дата назначения
Код:

CREATE TABLE ProjectAssignments (
    employee_id INTEGER REFERENCES Employees(id),
    project_id INTEGER REFERENCES Projects(id),
    assignment_date DATE DEFAULT CURRENT_DATE,
    PRIMARY KEY (employee_id, project_id)
);

<img width="623" height="480" alt="HW-12-1-01" src="https://github.com/user-attachments/assets/16975d9e-6588-4f04-b693-234a0cf43c7d" />


Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению. Вы можете их выполнить, если хотите глубже и шире разобраться в материале.

# Задание 2*
Разверните СУБД Postgres на своей хостовой машине, на виртуальной машине или в контейнере docker.
Опишите схему, полученную в предыдущем задании, с помощью скрипта SQL.
Создайте в вашей полученной СУБД новую базу данных и выполните полученный ранее скрипт для создания вашей модели данных.
В качестве решения приложите SQL скрипт и скриншот диаграммы.

Для написания и редактирования sql удобно использовать специальный инструмент dbeaver.
