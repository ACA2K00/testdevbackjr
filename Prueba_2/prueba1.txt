CREATE DATABASE Oficina;
USE Oficina;

CREATE TABLE usuarios (
    userId INT NOT NULL PRIMARY KEY,
    Login VARCHAR(100) NOT NULL,
    Nombre VARCHAR(100) NOT NULL,
    Paterno VARCHAR(100) NOT NULL,
    Materno VARCHAR(100) NOT NULL
);

CREATE TABLE empleados (
    userId INT NOT NULL,
    Sueldo DOUBLE NOT NULL,
    FechaIngreso DATE NOT NULL
);

/*Datos importados a usuarios utilizando la herramienta Table Data Import Wizard*/
SELECT 
    *
FROM
    usuarios;

INSERT INTO empleados
(userId, Sueldo, FechaIngreso)
VALUES
(1,8837,'2000-01-11'),
(2,8837,'2000-01-11'),
(3,15000,'2000-01-11'),
(4,15000,'2000-01-11'),
(5,7812,'2000-01-18'),
(6,7812,'2000-01-18'),
(7,10200,'2000-01-18'),
(8,10200,'2000-01-18'),
(9,13800,'2001-05-20'),
(10,13800,'2001-05-20'),
(11,18880,'2001-05-20'),
(12,18880,'2001-05-20'),
(13,8000,'2001-07-13'),
(14,8000,'2001-07-13'),
(15,6000,'2001-07-13'),
(16,19470,'2001-07-13'),
(17,19470,'2001-07-13'),
(18,10200,'2001-07-16'),
(19,10200,'2001-07-16'),
(20,25000,'2001-07-16'),
(21,7812,'2001-07-16'),
(22,7812,'2001-07-16'),
(23,12210,'2001-11-24'),
(24,12210,'2001-11-24'),
(25,7500,'2001-11-24'),
(26,15020,'2001-11-24'),
(27,15020,'2001-11-24'),
(28,25000,'2001-11-24'),
(29,7812,'2001-11-24'),
(30,15020,'2001-12-12'),
(31,15020,'2001-12-12'),
(32,12210,'2001-12-12'),
(33,12210,'2001-12-12'),
(34,19470,'2008-08-17'),
(35,19470,'2008-08-17'),
(36,8000,'2008-08-17'),
(37,8000,'2008-08-17'),
(38,18880,'2009-06-11'),
(39,18880,'2009-06-11'),
(40,14000,'2009-06-11'),
(41,13800,'2009-06-11'),
(42,13800,'2009-06-11'),
(43,15000,'2009-10-06'),
(44,15000,'2009-10-06'),
(45,13000,'2009-10-06'),
(46,8837,'2009-10-06');

/*Depurar solo los ID diferentes de 6,7,9 y 10 de la tabla usuarios (5 puntos)*/
DELETE FROM usuarios 
WHERE
    NOT (userId = 6 OR userId = 7 OR userId = 9
    OR userId = 10);

/*Actualizar el dato Sueldo en un 10 porciento a los empleados que tienen fechas entre el año
2000 y 2001 (5 puntos)*/
SELECT 
    *
FROM
    empleados
WHERE
    YEAR(FechaIngreso) = 2000
        OR YEAR(FechaIngreso) = 2001
UPDATE empleados 
SET 
    Sueldo = Sueldo + (Sueldo * 0.10)
WHERE
    YEAR(FechaIngreso) = 2000
        OR YEAR(FechaIngreso) = 2001
SELECT 
    *
FROM
    empleados
WHERE
    YEAR(FechaIngreso) = 2000
        OR YEAR(FechaIngreso) = 2001

/*Realiza una consulta para traer el nombre de usuario y fecha de ingreso de los usuarios que
gananen mas de 10000 y su apellido comience con T ordernado del mas reciente al mas antiguo
(10 puntos)*/
SELECT 
    usuarios.Nombre, usuarios.Paterno, empleados.FechaIngreso
FROM
    empleados
        INNER JOIN
    usuarios ON empleados.userId = usuarios.userId
WHERE
    Sueldo > 10000
        AND usuarios.Paterno LIKE 'T%'
ORDER BY empleados.FechaIngreso DESC

/*Realiza una consulta donde agrupes a los empleados por sueldo, un grupo con los que ganan
menos de 12000 y uno mayor o igual a 12000, cuantos hay en cada grupo? (10 puntos)*/
SELECT 
    COUNT(Sueldo)
FROM
    empleados
GROUP BY Sueldo > 12000 , Sueldo < 12000