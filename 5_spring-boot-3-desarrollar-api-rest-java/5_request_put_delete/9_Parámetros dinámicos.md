Estás trabajando en una aplicación con Spring Boot y te encuentras con el siguiente método:

@DeleteMapping(“/id”)
public void eliminar(@PathVariable Long id) {
    repository.deleteById(id);
}COPIA EL CÓDIGO
Teniendo en cuenta que la clase Controller a la que pertenece este método está anotada con @RequestMapping(“/productos”), ¿qué sucederá si se activa una solicitud DELETE en la API con la url /productos/0?

Seleccione una alternativa

Ocurrirá un error porque el id se pasó con el valor 0 (cero), y en la base de datos los ID deben empezar por 1.


El producto no se eliminará de la base de datos, ya que el método no se anotó con @Transactional.


Se producirá un error 404 - not found.