En una clase Controller existe el siguiente método declarado:

@PostMapping
public void registrar(DatosRegistroProducto datos) {
    System.out.println(datos);
}COPIA EL CÓDIGO
Y en este proyecto también se creó el DTO DatosRegistroProducto:

public record DatosRegistroProducto(String nombre, String descripcion, BigDecimal precio){}COPIA EL CÓDIGO
Realizas una solicitud POST y envías el siguiente JSON en su cuerpo:

{
    “precio” : 399.99,
    “descripcion” : “Wireless. Color: blanco”,
    “nombre” : “Audifonos”
}COPIA EL CÓDIGO
Pero, al verificar la consola del IDE, se da cuenta de que todos los datos llegan como nulos.

Elija la alternativa CORRECTA que indica por qué los datos se devuelven como nulos:

Seleccione una alternativa

Faltó anotar el parámetro datos, recibido en el método registrar del Controller, con @RequestBody.


Falta indicar en el método del Controller de que la solicitud recibirá datos en formato JSON.


El orden de los campos en el JSON no es el mismo que el declarado en el DTO.