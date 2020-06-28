# Rango denso

Agrupa y ordena por rentas las peliculas dandole una posicion dentro del top.

    SELECT
        peliculas.pelicula_id AS id,
        peliculas.titulo,
        COUNT(*) AS numero_rentas,
        DENSE_RANK () OVER (					--Windows Functions nos permite reindexar las filas over permite saber como se hara.
            ORDER BY COUNT (*) DESC
        ) AS posicion
    FROM rentas
        INNER JOIN inventarios ON rentas.inventario_id = inventarios.inventario_id
        INNER JOIN peliculas ON inventarios.pelicula_id = peliculas.pelicula_id
    GROUP BY peliculas.pelicula_id
    ORDER BY numero_rentas DESC;