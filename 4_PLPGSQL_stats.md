# PLPGSQL STATS

1. Funcion que retorna estadisticas

        CREATE OR REPLACE FUNCTION movies_stats()		-- Funcion que retorna valores descriptivos
        RETURNS VOID									 -- Returna nulo
        LANGUAGE PLPGSQL								 -- Se trabaja con PLPGSQL lenguaje
        AS $$											 -- Se abre el cuerpo de la funcion
        DECLARE											 -- Se abre declaracion de variables inicializacion
            total_rated_r 			REAL := 0.0;
            total_larger_than_100   REAL := 0.0;
            total_published_2006    REAL := 0.0;
            average_duration		REAL := 0.0;
            average_rental_price	REAL := 0.0;
        BEGIN											 -- Se comienza las transformaciones
            total_rated_r 			:= COUNT(*) FROM peliculas WHERE clasificacion = 'R';
            total_larger_than_100   := COUNT(*) FROM peliculas WHERE duracion > 100;
            total_published_2006	:= COUNT(*) FROM peliculas WHERE anio_publicacion = 2006;
            average_duration		:= AVG(duracion) FROM peliculas;
            average_rental_price	:= AVG(precio_renta) FROM peliculas;
            
            TRUNCATE TABLE peliculas_estadisticas;		 -- Vacia la tabla que ya existe
            
            INSERT INTO peliculas_estadisticas(tipo_estadistica, total) -- Se ingresa los datos creados en la tabla
            VALUES 
                ('Peliculas con clasificacion R',total_rated_r),
                ('Peliculas de mas de 100 minutos',total_larger_than_100),
                ('Peliculas publicadas en 2006',total_published_2006),
                ('Promedio de duracion en minutos',average_duration),
                ('Promedio de precio renta',average_rental_price);
        END
        $$;


        SELECT movies_stats()							-- Ejecuta la funcion