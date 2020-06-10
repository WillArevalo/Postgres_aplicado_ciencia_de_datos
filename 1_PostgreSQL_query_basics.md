# Query Basics

    SELECT MAX(ultima_actualizacion) AS fecha_ultima_actualizacion,   -- Select trae las columnas que deseo
        clasificacion,												  -- AS es un alias
        COUNT(*) AS cantidad_peliculas								  -- Count cuenta todos los registros de una consulta
    FROM	peliculas												  -- From nos dice de que tabla(s) se traen las columnas
    WHERE 	duracion_renta > 3										  -- Where nos permite traer informacion condicionada
    GROUP BY	clasificacion, ultima_actualizacion					  -- Group by nos permite agrupar informacion
    ORDER BY	fecha_ultima_actualizacion DESC;					  -- Order by ordena dada una columna