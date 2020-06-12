# Conteo, Registros y Triggers

1. Funcion que solamente retorna un numero

        CREATE OR REPLACE FUNCTION count_total_movies()		-- Esta funcion retorna un solo valor en vez de una tabla
        RETURNS int										
        LANGUAGE PLPGSQL										 
        AS $$													 
        BEGIN
            RETURN COUNT (*) FROM peliculas;
        END
        $$;														 


        SELECT * FROM count_total_movies();

2. Funcion amarrada a un trigger

        CREATE OR REPLACE FUNCTION duplicate_records()			-- Crea o reemplaza funcion para duplicar registros en otra tabla
        RETURNS TRIGGER
        LANGUAGE PLPGSQL
        AS $$
        BEGIN
            INSERT INTO aaab(bbba, ccca)							-- Inserta los valores a una tabla respaldo en el momento
            VALUES (NEW.bbb, NEW.ccc);							-- new significa los valores que se estan insertando en la tabla principal
            RETURN NEW;
        END
        $$;


        CREATE TRIGGER aaa_changes								-- Se crea el trigger disparador
            BEFORE INSERT										-- Se disparara antes de insertar
            ON aaa												-- sobre la tabla aaa
            FOR EACH ROW										-- para cada fila registro
            EXECUTE PROCEDURE duplicate_records();				-- Ejecutara el procedimiento/funcion
            

        -- Se ingresa un registro en la tabla principal para probar

        INSERT INTO aaa(bbb, ccc)
        VALUES ('ASDFG','HJKLM');