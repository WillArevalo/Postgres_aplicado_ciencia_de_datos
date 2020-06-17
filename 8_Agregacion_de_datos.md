# Agregacion de datos

_Las agregaciones son una serie de operaciones que se pueden hacer a las columnas _Es prioritario hacer una agrupacion para que aparezcan los datos por categorias__

- SUM()
- MIN()
- MAX()
- AVG()
- COUNT()


1. Query: _Promedio de duracion de la renta por categoria_

        SELECT c.categoria_id, c.nombre, AVG(p.duracion_renta) as Promedio_Duracion_Renta
        FROM peliculas AS p
        JOIN peliculas_categorias AS pc ON pc.pelicula_id = p.pelicula_id
        JOIN categorias AS c ON c.categoria_id = pc.categoria_id
        GROUP BY c.categoria_id, c.nombre
        ORDER BY Promedio_Duracion_Renta DESC;

2. Query: _Total Renta por Categoria_

        SELECT c.categoria_id, c.nombre, SUM(p.precio_renta) AS Renta_Categoria
        FROM peliculas AS p
        JOIN peliculas_categorias AS pc ON pc.pelicula_id = p.pelicula_id
        JOIN categorias AS c ON c.categoria_id = pc.categoria_id
        GROUP BY c.categoria_id, c.nombre
        ORDER BY Renta_Categoria DESC;

3. Query: _Conteo de peliculas por año de publicacion_

        SELECT anio_publicacion, COUNT(*)
        FROM peliculas
        GROUP BY anio_publicacion;
        ORDER BY anio_publicacion DESC;

4. Query: _Precios de renta máximo, mínimo y promedio_

        SELECT MAX(precio_renta), MIN(precio_renta), AVG(precio_renta)
        FROM peliculas;

5. Query: _Cantidad de transacciones por cliente_

        SELECT cliente_id, COUNT (renta_id) AS Transacciones
        FROM pagos
        GROUPBY cliente_id
        ORDERBY Transacciones DESC;