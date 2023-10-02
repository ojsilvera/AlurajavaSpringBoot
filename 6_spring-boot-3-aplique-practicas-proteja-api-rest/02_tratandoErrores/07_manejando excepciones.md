En un proyecto de una API Rest con Spring Boot, el manejo personalizado del Error 404 no se está realizando correctamente, a pesar de que existe la siguiente clase en ese proyecto:

@RestController
public class ExceptionHandler {

    @ExceptionHandler(EntityNotFoundException.class)
    public void handleErro404() {
    }

}COPIA EL CÓDIGO
¿Por qué no se ejecuta el método handleErro404 de esta clase?

Seleccione una alternativa

La excepción pasada en la anotación @ExceptionHandler es del tipo sin unchecked.


La clase no se anotó con @Configuration.


La clase se anotó incorrectamente.


El retorno del método fue declarado como nulo.