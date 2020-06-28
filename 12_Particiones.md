# Particiones

Permiten segmentar los datos para que sea mas facil encontrarlos a la hora de consultarlos.

ex. Particionamos la tabla por la columna mes, lo cual nos permitira una mayor velocidad de consulta debido que buscara en solo una parte de la tabla y no en toda la tabla.

Vale la pena particionalas cuando hablamos de millones de datos por particiones.


Una desventaja es que se pierden las claves primarias a la hora de consultar ya que consultan por segmentos y tardaran mas.