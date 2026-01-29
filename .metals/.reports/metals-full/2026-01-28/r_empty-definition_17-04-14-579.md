error id: file://<WORKSPACE>/src/main/java/com/example/agent/web/UserControllerIT.java:org/assertj/core/api/Assertions#
file://<WORKSPACE>/src/main/java/com/example/agent/web/UserControllerIT.java
empty definition using pc, found symbol in pc: org/assertj/core/api/Assertions#
empty definition using semanticdb
empty definition using fallback
non-local guesses:

offset: 338
uri: file://<WORKSPACE>/src/main/java/com/example/agent/web/UserControllerIT.java
text:
```scala
package com.example.agent.web;

import com.example.agent.domain.User;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.reactive.server.WebTestClient;

import static org.assertj.core.api.Assert@@ions.assertThat;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class UserControllerIT {

    @Autowired
    WebTestClient web;

    @Test
    void should_create_and_get_user() {
        // 1) Create a user
        User created = web.post()
                .uri(uriBuilder -> uriBuilder
                        .path("/api/users")
                        .queryParam("name", "Alice")
                        .queryParam("email", "alice@example.com")
                        .build())
                .exchange()
                .expectStatus().isOk()
                .expectBody(User.class)
                .returnResult()
                .getResponseBody();

        assertThat(created).isNotNull();
        assertThat(created.id()).isNotBlank();
        assertThat(created.name()).isEqualTo("Alice");
        assertThat(created.email()).isEqualTo("alice@example.com");

        // 2) Retrieve the user by id
        User fetched = web.get()
                .uri("/api/users/{id}", created.id())
                .exchange()
                .expectStatus().isOk()
                .expectBody(User.class)
                .returnResult()
                .getResponseBody();

        assertThat(fetched).isNotNull();
        assertThat(fetched.id()).isEqualTo(created.id());
        assertThat(fetched.name()).isEqualTo("Alice");
        assertThat(fetched.email()).isEqualTo("alice@example.com");
    }
}
```


#### Short summary: 

empty definition using pc, found symbol in pc: org/assertj/core/api/Assertions#