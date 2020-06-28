# Trigger de conversion de precios a pesos mexicanos

Funcion

    CREATE OR REPLACE FUNCTION public.precio_peliculas_tipo_cambio()
        returns trigger
        LANGUAGE plpgsql
    AS $$
        BEGIN
            INSERTINTO precio_peliculas_tipo_cambio(
            pelicula_id,
            tipo_cambio_id,
            precio_tipo_cambio,
            ultima_actualizacion
            )
            selectNEW.pelicula_id,
                    tipos_cambio.tipo_cambio_id,
                    tipos_cambio.cambio_usd * NEW.precio_renta AS precio_tipo_cambio,
                    CURRENT_TIMESTAMP
            FROM tipos_cambio
            WHERE tipos_cambio.codigo = 'MXN';
            RETURN NEW;
        END
    $$
    ;

___

Trigger

    CREATE TRIGGER trigger_update_tipos_cambio 
        AFTER INSERT O UPDATE
	    ON public.peliculas 
        FOR EACH ROW 
        EXECUTE PROCEDURE public.precio_peliculas_tipo_cambio();