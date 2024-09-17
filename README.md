CREATE TABLE Aerolineas (
    id_aerolinea INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    codigo VARCHAR(10) NOT NULL UNIQUE,
    pais VARCHAR(50) NOT NULL
);
CREATE TABLE Vuelos (
    id_vuelo INT AUTO_INCREMENT PRIMARY KEY,
    id_aerolinea INT,
    numero_vuelo VARCHAR(10) NOT NULL UNIQUE,
    origen VARCHAR(50) NOT NULL,
    destino VARCHAR(50) NOT NULL,
    fecha_salida DATETIME NOT NULL,
    fecha_llegada DATETIME NOT NULL,
    estado ENUM('programado', 'en vuelo', 'cancelado', 'retrasado', 'completado') NOT NULL,
    FOREIGN KEY (id_aerolinea) REFERENCES Aerolineas(id_aerolinea)
);
CREATE TABLE Pasajeros (
    id_pasajero INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    fecha_nacimiento DATE NOT NULL,
    pasaporte VARCHAR(20) NOT NULL UNIQUE,
    nacionalidad VARCHAR(50) NOT NULL
);
CREATE TABLE Reservas (
    id_reserva INT AUTO_INCREMENT PRIMARY KEY,
    id_vuelo INT,
    id_pasajero INT,
    fecha_reserva DATETIME NOT NULL,
    asiento VARCHAR(5) NOT NULL,
    clase ENUM('economica', 'premium', 'business', 'primera') NOT NULL,
    estado ENUM('confirmada', 'pendiente', 'cancelada') NOT NULL,
    FOREIGN KEY (id_vuelo) REFERENCES Vuelos(id_vuelo),
    FOREIGN KEY (id_pasajero) REFERENCES Pasajeros(id_pasajero)
);
CREATE TABLE AsignacionPersonal (
    id_asignacion INT AUTO_INCREMENT PRIMARY KEY,
    id_vuelo INT,
    id_empleado INT,
    rol VARCHAR(50) NOT NULL,
    FOREIGN KEY (id_vuelo) REFERENCES Vuelos(id_vuelo),
    FOREIGN KEY (id_empleado) REFERENCES Empleados(id_empleado)
);
