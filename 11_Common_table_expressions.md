# Common table expressions



- Es una herramienta que usa expresiones de tablas para agilizar en postgres cálculos en casos de uso específicos.

- Ofrecen una mayor aplicabilidad a casos de usos iterantes, casos en los cuales su estructura bajo lenguaje SQL es dispendiosa tanto en su construcción como su ejecución para el servidor.

- Es necesario ahondar más en este tema ya que su versatilidad es interesante.

[https://www.postgresql.org/docs/12/queries-with.html#QUERIES-WITH-SELECT]


    WITH RECURSIVE tabla_recursiva(n) AS (
        VALUES(1)
        UNION ALL
        SELECT n+1 FROM tabla_recursiva WHERE n < 100
    ) SELECT SUM(n) FROM tabla_recursiva;

Casos de uso iterar y transformar datos al pasar de una tabla a otra.