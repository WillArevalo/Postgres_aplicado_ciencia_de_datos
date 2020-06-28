# Datos Geograficos

Si necesitan mas informacion busquen PostGis

    select ciudades.ciudad_id,
        ciudades.ciudad,
        count(*) as renta_por_ciudad
    from   ciudades
        inner join direcciones on ciudades.ciudad_id = direcciones.ciudad_id
        inner join tiendas on tiendas.direccion_id = direcciones.direccion_id
        inner join inventarios on inventarios.tienda_id = tiendas.tienda_id
        inner join rentas on inventarios.inventario_id = rentas.inventario_id
    group by ciudades.ciudad_id;