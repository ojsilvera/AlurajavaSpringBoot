Un compañero de trabajo solicita su ayuda para identificar un problema en su código, relacionado con una clase de configuración de Spring Security:

@Configuration
@EnableWebSecurity
public class SecurityConfigurations {

    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http.csrf().disable()
                .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
                .and().build();
    }

}COPIA EL CÓDIGO
Afirma que, incluso después de crear esta clase, Spring Security sigue bloqueando todas las solicitudes que llegan a la API y devuelve el código HTTP 401 (Unauthorized).

Revise el código anterior y elija la opción que indica qué está causando este problema.

Seleccione una alternativa

El parámetro pasado al método sessionCreationPolicy debe ser SessionCreationPolicy.STATEFUL.


La clase no hereda de la clase SpringSecurityConfigurationsBean.


El método securityFilterChain debería haberse anotado con @Bean. *******


El método securityFilterChain debería haberse declarado como protected.