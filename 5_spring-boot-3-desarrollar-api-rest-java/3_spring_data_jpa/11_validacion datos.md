Está trabajando en un proyecto que utiliza Bean Validation, sin embargo, las validaciones no se realizan y la información llega a la base de datos de forma NO válida.

Revise los siguientes fragmentos de código de este proyecto:

@PostMapping
public void registrar(@RequestBody DatosRegistroProducto datos) {
    repository.save(new Producto(datos));
}COPIA EL CÓDIGO
public record DatosRegistroProducto(
        @NotBlank String nombre,
        @NotBlank String descripcion,
        @NotNull @DecimalMin("1.00") BigDecimal precio
) {
}COPIA EL CÓDIGO
Elija la alternativa CORRECTA que identifica el problema mencionado:

Seleccione una alternativa

Faltó anotar el parámetro datos, recibido en el método registrar del Controller con @Valid.


El método registrar se declaró con un retorno void.


Faltó colocar en el método registro la anotación @Transactional.