@PostMapping
@Transactional
public ResponseEntity registrar(@RequestBody @Valid DatosRegistroProducto datos) {
    var producto = new Producto(datos);
    repository.save(producto);

    var uri = new URI("/productos/{id}");

    return ResponseEntity.ok(new DatosDetalladoProducto(producto));
}COPIA EL CÓDIGO
Teniendo en cuenta las buenas prácticas de retorno en una solicitud HTTP de tipo POST, elige las alternativas que indican los problemas en el código anterior:

Selecciona 2 alternativas

El Header Location se creará incorrectamente.*


El código anterior no devolverá el código 201 como respuesta.*


No se realizará la validación de información.


No se devolverá una representación del recurso creado en la API.