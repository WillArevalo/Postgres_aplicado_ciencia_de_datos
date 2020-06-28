# Agregacion de datos JSON

[Excelentes tecnicas CRUD para JSONB](https://www.enterprisedb.com/es/blog/crud-json-postgresql)

Encontrando el valor minimo, se debe castear primero (Convertir un objecto de un  tipo en otro)


    SELECT
        MIN(
            CAST(
                info -> 'items' ->> 'cantidad' AS INTEGER
            )
        ) as Minimo_nro_items_x_cliente
        
    FROM ordenes;

____

    SELECT
        MIN(
            CAST(
                info -> 'items' ->> 'cantidad' AS INTEGER
            )
        ) as Minimo_nro_items_x_cliente,
        MAX(
            CAST(
                info -> 'items' ->> 'cantidad' AS INTEGER
            )
        ) as Maximo_nro_items_x_cliente,
        SUM(
            CAST(
                info -> 'items' ->> 'cantidad' AS INTEGER
            )
        ) as Suma_nro_items_x_cliente,
        AVG(
            CAST(
                info -> 'items' ->> 'cantidad' AS INTEGER
            )
        ) as Promedio_nro_items_x_cliente	
    FROM ordenes;
