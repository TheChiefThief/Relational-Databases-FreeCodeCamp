# 🗄️ SQL Terminal Mastery: Command Line Guide

![SQL](https://img.shields.io/badge/SQL-Terminal-blue?style=for-the-badge&logo=sqlite&logoColor=white)
![Database](https://img.shields.io/badge/DB-Admin-orange?style=for-the-badge&logo=mysql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)

Este documento es un **manual práctico** para trabajar con **SQL desde la terminal**. Está pensado para bases de datos relacionales comunes (MySQL/MariaDB, PostgreSQL y SQLite). Donde haya diferencias importantes, se aclaran explícitamente.

---

## 1. Requisitos previos

Antes de comenzar, necesitás:

* Conocimientos básicos de terminal (cd, ls, pwd, etc.)
* Tener instalado al menos **un motor de base de datos**:

  * MySQL / MariaDB
  * PostgreSQL
  * SQLite

Verificá la instalación:

```bash
mysql --version
psql --version
sqlite3 --version
```

---

## 2. Acceder a SQL desde la terminal

### 2.1 MySQL / MariaDB

```bash
mysql -u usuario -p
```

* `-u`: usuario
* `-p`: solicita contraseña

Conectar a una base específica:

```bash
mysql -u usuario -p nombre_db
```

---

### 2.2 PostgreSQL

```bash
psql -U usuario
```

Conectar a una base específica:

```bash
psql -U usuario -d nombre_db
```

---

### 2.3 SQLite

```bash
sqlite3 archivo.db
```

Si el archivo no existe, se crea automáticamente.

---

## 3. Comandos básicos de la consola SQL

### 3.1 Salir del cliente

| Motor      | Comando           |
| ---------- | ----------------- |
| MySQL      | `exit;` o `quit;` |
| PostgreSQL | `\q`              |
| SQLite     | `.exit`           |

---

### 3.2 Ayuda

* MySQL:

```sql
HELP;
```

* PostgreSQL:

```sql
\h
```

* SQLite:

```sql
.help
```

---

## 4. Gestión de bases de datos

### 4.1 Listar bases de datos

```sql
SHOW DATABASES;        -- MySQL
\l                     -- PostgreSQL
.databases             -- SQLite
```

---

### 4.2 Crear una base de datos

```sql
CREATE DATABASE empresa;
```

---

### 4.3 Usar una base de datos

```sql
USE empresa;           -- MySQL
\c empresa              -- PostgreSQL
```

(SQLite usa una base por archivo)

---

### 4.4 Eliminar una base de datos

```sql
DROP DATABASE empresa;
```

⚠️ Operación irreversible.

---

## 5. Gestión de tablas

### 5.1 Crear tabla

```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    salario DECIMAL(10,2),
    fecha_ingreso DATE
);
```

---

### 5.2 Ver tablas

```sql
SHOW TABLES;           -- MySQL
\dt                     -- PostgreSQL
.tables                 -- SQLite
```

---

### 5.3 Describir estructura

```sql
DESCRIBE empleados;    -- MySQL
\d empleados            -- PostgreSQL
PRAGMA table_info(empleados); -- SQLite
```

---

### 5.4 Eliminar tabla

```sql
DROP TABLE empleados;
```

---

## 6. Operaciones CRUD

### 6.1 INSERT (Crear registros)

```sql
INSERT INTO empleados (id, nombre, salario, fecha_ingreso)
VALUES (1, 'Juan Pérez', 150000, '2023-01-10');
```

---

### 6.2 SELECT (Leer datos)

```sql
SELECT * FROM empleados;
```

Seleccionar columnas específicas:

```sql
SELECT nombre, salario FROM empleados;
```

---

### 6.3 WHERE (Filtrar datos)

```sql
SELECT * FROM empleados
WHERE salario > 120000;
```

---

### 6.4 UPDATE (Actualizar datos)

```sql
UPDATE empleados
SET salario = 180000
WHERE id = 1;
```

---

### 6.5 DELETE (Eliminar datos)

```sql
DELETE FROM empleados
WHERE id = 1;
```

⚠️ Sin WHERE elimina todos los registros.

---

## 7. Ordenamiento y límites

### 7.1 ORDER BY

```sql
SELECT * FROM empleados
ORDER BY salario DESC;
```

---

### 7.2 LIMIT / OFFSET

```sql
SELECT * FROM empleados
LIMIT 5 OFFSET 10;
```

---

## 8. Funciones agregadas

```sql
SELECT COUNT(*) FROM empleados;
SELECT AVG(salario) FROM empleados;
SELECT MAX(salario) FROM empleados;
SELECT MIN(salario) FROM empleados;
```

---

## 9. GROUP BY y HAVING

```sql
SELECT fecha_ingreso, COUNT(*)
FROM empleados
GROUP BY fecha_ingreso;
```

```sql
SELECT fecha_ingreso, COUNT(*)
FROM empleados
GROUP BY fecha_ingreso
HAVING COUNT(*) > 1;
```

---

## 10. Relaciones y claves foráneas

```sql
CREATE TABLE departamentos (
    id INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    departamento_id INT,
    FOREIGN KEY (departamento_id) REFERENCES departamentos(id)
);
```

---

## 11. JOINs

### 11.1 INNER JOIN

```sql
SELECT e.nombre, d.nombre
FROM empleados e
INNER JOIN departamentos d
ON e.departamento_id = d.id;
```

---

### 11.2 LEFT JOIN

```sql
SELECT e.nombre, d.nombre
FROM empleados e
LEFT JOIN departamentos d
ON e.departamento_id = d.id;
```

---

## 12. Ejecutar scripts SQL desde archivos

```bash
mysql -u usuario -p db < script.sql
psql -U usuario -d db -f script.sql
sqlite3 db.sqlite < script.sql
```

---

## 13. Redirección de resultados a archivos

```bash
mysql -u usuario -p -e "SELECT * FROM empleados" db > salida.txt
```

---

## 14. Buenas prácticas

* Usar `WHERE` siempre que sea posible
* Hacer backups antes de `UPDATE` o `DELETE`
* Nombrar tablas y columnas de forma clara
* Evitar `SELECT *` en producción

---

## 15. Errores comunes

* Olvidar `;` al final de la sentencia
* Usar `DELETE` sin `WHERE`
* Confundir `CHAR` con `VARCHAR`
* No validar claves foráneas

---

## 16. Recursos recomendados

* Documentación oficial MySQL
* Documentación oficial PostgreSQL
* [https://www.sqlite.org/docs.html](https://www.sqlite.org/docs.html)

---

## 17. Conclusión

Este README sirve como **manual base de SQL en la terminal**. SQL se aprende practicando: ejecutá comandos, rompé cosas en entornos de prueba y analizá los resultados.

Si necesitás una versión avanzada (índices, transacciones, CTEs, ventanas, optimización), este manual se puede extender fácilmente.
