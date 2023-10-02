¡Atención!
En la versión final 3.0.0 de Spring Boot se realizó un cambio en Spring Security, en cuanto a códigos que restringen el control de acceso. A lo largo de las clases, el método securityFilterChain(HttpSecurity http), declarado en la clase SecurityConfigurations, tenía la siguiente estructura:

@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http.csrf().disable()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and().authorizeRequests()
            .antMatchers(HttpMethod.POST, "/login").permitAll()
            .anyRequest().authenticated()
            .and().build();
}COPIA EL CÓDIGO
Sin embargo, desde la versión final 3.0.0 de Spring Boot, el método authorizeRequests() ha quedado obsoleto y debe ser reemplazado por el nuevo método authorizeHttpRequests(). Asimismo, el método antMatchers() debería ser reemplazado por el nuevo método requestMatchers():

@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http.csrf().disable()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and().authorizeHttpRequests()
            .requestMatchers(HttpMethod.POST, "/login").permitAll()
            .anyRequest().authenticated()
            .and().build();
}