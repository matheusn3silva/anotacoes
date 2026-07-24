# Anotações sobre Spring Web e Criação de Rotas
---


Para criar rotas web, primeiro precisamos importar as anotações:

```java
import org.springframework.web.bind.annotation.*;
```

Isso permitirá utilizarmos as anotações de métodos HTTPs que vamos utilizar no nosos Controller.


```java
@GetMapping // Define rota GET
@PostMapping // Define rota POST
@PutMapping // Define rota PUT
@DeleteMapping // Define rota DELETE
```

### Exemplos de rotas em um Controller

```java

import org.springframework.web.bind.annotation.*;
import org.springframework.http.HttpStatus;

@RestController
@RequestMapping('/v1/user')
public class UserController {

    @GetMapping 
    public String getAllUsers {
        return "Retorna todos usuários";
    }

    @GetMapping("/{id}") // Cria uma nova rota, agora esperando um ID
    @ResponseStatus(HttpStatus.OK) // Define o Status HTTP retornado na mensagem OK = 200
    public String getUser {
        return "Retorna somente um usuário";
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED) // CREATE = 201
    public String postUser(@RequestBody String name) { // Aqui definimos que usaremos o conteudo do body para criar um usuário
        return "Usuário: " + name + " criado com SUCESSO!";
    }
}
```

---


### Abaixo deixo outras formas de criar as rotas e definir os status HTTP

```java
@GetMapping // Metodo GET
public String helloWorld() {
    return "Hello World!";
}

@GetMapping
public ResponseEntity<String> helloWorld() { // ResponseEntity obriga a definir o metodo HTTP na mensagem
    return ResponseEntity.ok("Hello, World!"); // ok = 200
}

// Aqui utilizamos o NEW para definir o conteúdo retornado e o status HTTP
@GetMapping
public ResponseEntity<String> helloWorld() {
    return new ResponseEntity<>("Hello, World!", HttpStatus.OK);
}
```