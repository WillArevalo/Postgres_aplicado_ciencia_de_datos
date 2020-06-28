# Trabajando con JSON y BSON en PostgreSQL

_PostgreSQL como manejador de BD tambien nos permite trabajar con datos de tipos objetos como son JSON y JSONB(JSON binario lo que permite mas agilidad transaccional que se pierde al leer una cadena para extraer diferentes argumentos). Los objetos JSON no son mas que cadenas de caracteres(strings) que se identifican en forma de clave valor_

1. Query: _Creando una tabla, insertando y consultando JSON_

        CREATE TABLE ordenes (                              -- Crea una tabla con un ID e info de tipo JSON
            ID serial NOT NULL PRIMARY KEY,                 -- Autoincremental, no puede ser vacio, y es llave primaria
            info json NOT NULL                              -- info es un campo de tipo JSON si quisieramos que ademas fuese binario se coloca jsonb    
        );


        INSERT INTO ordenes(info)
        VALUES
            (
                '{"cliente":"David Sanchez", "items":{"producto":"Biberón", "cantidad":"24"}}'
            ),
            (
                '{"cliente":"Edna Cardenas", "items":{"producto":"Carro juguete", "cantidad":"1"}}'
            ),
            (
                '{"cliente":"William Arevalo", "items":[{"producto":"Tren juguete", "cantidad":"1"},{"producto":"Biberón", "cantidad":"2"}]}'
            );

        SELECT
            info -> 'cliente' as Cliente
        FROM ordenes;

        SELECT
            info ->> 'cliente' AS cliente
        FROM ordenes
        WHERE info -> 'items' ->> 'producto' = 'Biberón';
