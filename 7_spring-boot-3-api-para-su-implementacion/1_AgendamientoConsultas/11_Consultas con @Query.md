Al analizar el código de una interfaz repository en un proyecto con Spring Boot, se encuentra el siguiente método:

@Query(“””
select p from Producto p
where
p.precio >= :precio
and
p.fecha>= fecha
“””)
List<Producto> buscarPorPrecioyFecha(BigDecimal preco, LocalDate fecha);COPIA EL CÓDIGO
¿Cuál es el problema existente en el método anterior?

Seleccione una alternativa

No se puede utilizar el operador >= para atributos del tipo fecha.


Faltó agregar el caracter dos-puntos (:) antes del parámetro fecha.*************


El nombre del método no sigue el estándar de nomenclatura de Spring Data.


El retorno del método debería ser Producto y no List<Producto>.