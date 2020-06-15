# Tipos de datos personalizados

Crear estos tipos de datos personalizados nos da muchas mas opciones mas que solo indicar si un dato debe ser entero, string, etc. Tambien tenemos la posibilidad de limitar las opciones de el registro, algo asi como una lista desplegable que solo nos deja seleccionar un solo dato, en el lenguaje SQL insertar valores espcificos de una lista de valores definidos al momento de crear nuestro tipo de dato.

Crear dato tipo lista: CREATE TYPE + nombre_lista + AS ENUM ('valores lista')

        CREATE TYPE humor AS ENUM ('triste', 'normal', 'feliz');	-- Crea un nuevo tipo de dato, normalmente de lista.

        CREATE TABLE persona_prueba(								-- Crea una nueva tabla con el dato custom.
            nombre text,
            humor_actual humor
        );

        INSERT INTO persona_prueba(nombre, humor_actual)			-- Insert de prueba si es diferente a los valores del enum bota error.
            VALUES ('william', 'feliz');