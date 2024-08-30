- 👋 Hi, I’m @Daniela1724
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Daniela1724/Daniela1724 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

CREATE DATABASE Empresa;
USE Empresa;
CREATE TABLE Empleados (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Nombre VARCHAR(50) NOT NULL,
    Apellido VARCHAR(50) NOT NULL,
    FechaContratacion DATE,
    Cargo VARCHAR(50)
);
INSERT INTO Empleados (Nombre, Apellido, FechaContratacion, Cargo)
VALUES 
    ('Juan', 'Pérez', '2023-01-15', 'Desarrollador'),
    ('Ana', 'Gómez', '2022-11-23', 'Diseñadora'),
    ('Luis', 'Martínez', '2024-03-10', 'Analista'),
    ('Laura', 'Rodríguez', '2021-09-05', 'Gerente');

SELECT * FROM Empleados;
UPDATE Empleados
SET Cargo = 'Jefe de Proyecto'
WHERE Nombre = 'Juan' AND Apellido = 'Pérez';
DELETE FROM Empleados
WHERE Nombre = 'Luis' AND Apellido = 'Martínez';


DELETE FROM Empleados
WHERE Nombre = 'Luis' AND Apellido = 'Martínez';
CREATE TABLE Cargos (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    NombreCargo VARCHAR(50) NOT NULL UNIQUE
);
INSERT INTO Cargos (NombreCargo)
VALUES 
    ('Desarrollador'),
    ('Diseñadora'),
    ('Analista'),
    ('Gerente'),
    ('Jefe de Proyecto');
CREATE TABLE Empleados (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Nombre VARCHAR(50) NOT NULL,
    Apellido VARCHAR(50) NOT NULL,
    FechaContratacion DATE,
    CargoID INT,
    FOREIGN KEY (CargoID) REFERENCES Cargos(ID)
);

INSERT INTO Empleados (Nombre, Apellido, FechaContratacion, CargoID)
VALUES 
    ('Juan', 'Pérez', '2023-01-15', 5),  -- Supongamos que 'Jefe de Proyecto' tiene el ID 5
    ('Ana', 'Gómez', '2022-11-23', 2),   -- 'Diseñadora' tiene el ID 2
    ('Luis', 'Martínez', '2024-03-10', 3),-- 'Analista' tiene el ID 3
    ('Laura', 'Rodríguez', '2021-09-05', 4);-- 'Gerente' tiene el ID 4


SELECT e.ID, e.Nombre, e.Apellido, e.FechaContratacion, c.NombreCargo
FROM Empleados e
JOIN Cargos c ON e.CargoID = c.ID;
CREATE TABLE Cargos (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    NombreCargo VARCHAR(50) NOT NULL UNIQUE,
    Descripcion TEXT,
    Nivel INT
);
INSERT INTO Cargos (NombreCargo, Descripcion, Nivel)
VALUES 
    ('Desarrollador', 'Encargado del desarrollo de software', 2),
    ('Diseñadora', 'Responsable del diseño gráfico', 2),
    ('Analista', 'Analiza requisitos y procesos', 2),
    ('Gerente', 'Gestiona el equipo y los proyectos', 1),
    ('Jefe de Proyecto', 'Coordina proyectos y recursos', 1);
ALTER TABLE Empleados
ADD COLUMN Salario DECIMAL(10, 2);


UPDATE Empleados
SET Salario = 50000.00
WHERE Nombre = 'Juan' AND Apellido = 'Pérez';

UPDATE Empleados
SET Salario = 45000.00
WHERE Nombre = 'Ana' AND Apellido = 'Gómez';

UPDATE Empleados
SET Salario = 47000.00
WHERE Nombre = 'Luis' AND Apellido = 'Martínez';

UPDATE Empleados
SET Salario = 60000.00
WHERE Nombre = 'Laura' AND Apellido = 'Rodríguez';



SELECT Nombre, Apellido, FechaContratacion, c.NombreCargo, Salario
FROM Empleados e
JOIN Cargos c ON e.CargoID = c.ID;




CREATE TABLE Salarios (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    EmpleadoID INT,
    Salario DECIMAL(10, 2),
    FechaInicio DATE,
    FechaFin DATE,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleados(ID)
);

INSERT INTO Salarios (EmpleadoID, Salario, FechaInicio, FechaFin)
VALUES 
    (1, 50000.00, '2023-01-15', NULL), -- Salario para Juan Pérez
    (2, 45000.00, '2022-11-23', NULL), -- Salario para Ana Gómez
    (3, 47000.00, '2024-03-10', NULL), -- Salario para Luis Martínez
    (4, 60000.00, '2021-09-05', NULL); -- Salario para Laura Rodríguez

SELECT e.Nombre, e.Apellido, e.FechaContratacion, c.NombreCargo, s.Salario
FROM Empleados e
JOIN Cargos c ON e.CargoID = c.ID
JOIN Salarios s ON e.ID = s.EmpleadoID
WHERE s.FechaFin IS NULL; -- Selecciona solo los registros actuales


-- Primero, termina el salario anterior
UPDATE Salarios
SET FechaFin = '2024-08-30'
WHERE EmpleadoID = 1 AND FechaFin IS NULL;

-- Luego, añade el nuevo salario
INSERT INTO Salarios (EmpleadoID, Salario, FechaInicio, FechaFin)
VALUES (1, 52000.00, '2024-08-31', NULL);


