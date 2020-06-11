# PLPGSQL: Stored procedures


_PL/pgSQL es el lenguaje debirado del estandar SQL que Postgres creo para hacer programacion mas ordenada y procedural, enfoncandose en triggers y stored procedures_

Los procedures son una serie de pasos similares a una funcion __que no retornan ningun valor.__

En _PL/pgSQL_ existen functions y stored procedures, que en si son similares al ser una serie de pasos a ejecutar, sin embargo las functions retornan valores de salida y estan escritas en lenguaje estrictamente _Pl/pgSQL_ mientras que los stored procedures son un estandar de SQL.

1. Store Procedure

        CREATE OR REPLACE PROCEDURE test_dropcreate_procedure()				-- Create or replace, crea o reemplaza el procedure
        LANGUAGE SQL												 		-- Se especifica el lenguaje utilizado
        AS $$														 		-- AS y signos significan que se abre el espacio para crear el procedure
            DROP TABLE IF EXISTS aaa;								 		-- Este comando nos permite borrar una tabla si existe
            CREATE TABLE aaa(bbb char(5) CONSTRAINT firstkey PRIMARY KEY)	-- Crea una nueva tabla y le asigna los atributos y una llave primaria
        $$;																	-- Cierra el espacio para crear el procedure


        CALL test_dropcreate_procedure()									-- Call permite llamar el procedure

2. Function

        CREATE OR REPLACE FUNCTION test_dropcreate_function()	-- Crea o reemplaza una funcion
        RETURNS VOID												 -- Retorna vacio
        LANGUAGE PLPGSQL										 -- Definimos el tipo de lenguaje a utilizar
        AS $$													 -- Abre cuerpo de la funcion
        BEGIN
            DROP TABLE IF EXISTS aaa;
            CREATE TABLE aaa(bbb char(5) CONSTRAINT firstkey PRIMARY KEY, ccc char(5));
            DROP TABLE IF EXISTS aaab;
            CREATE TABLE aaab (bbba char(5) CONSTRAINT secondkey PRIMARY KEY, ccca char(5));
        END
        $$;														 -- Cierra cuerpo de la funcion



        SELECT * FROM test_dropcreate_function();				-- Ejecutamos la funcion cual si fuese una consulta