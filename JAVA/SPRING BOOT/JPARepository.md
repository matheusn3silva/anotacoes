# JPA Repository

Quando os métodos padrão do JpaRepository (como `findAll()`, `findById()` e `save()`) não são suficientes, podemos criar consultas personalizadas de duas formas:

Query Methods: o Spring gera automaticamente a consulta com base no nome do método.
JPQL `(@Query)`: escrevemos manualmente a consulta utilizando entidades e seus atributos.

```java
package com.manasi.spring_boot_study.database.repository;

import com.manasi.spring_boot_study.database.model.ExerciciosEntity;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

import java.util.List;

public interface IExerciciosRepository extends JpaRepository<ExerciciosEntity, Integer> {

    // Query Method (consulta gerada automaticamente pelo Spring Data JPA)
    List<ExerciciosEntity> findAllByGrupoMuscular(String GrupoMuscular);

    // JPQL (consulta escrita manualmente utilizando entidades Java)
   @Query(value = """
        SELECT e
        FROM ExerciciosEntity e
        WHERE UPPER(e.grupoMuscular) = UPPER(:grupoMuscular)
    """)
    List<ExerciciosEntity> findAllByGrupoMuscularJPQL(@Param("grupoMuscular") String grupoMuscular);

    // Native Query (Consulta escrita manualmente utilizando linguagem padrão SQL)
    @NativeQuery(value = """
        SELECT e
        FROM exercicios e
        WHERE UPPER(e.grupo_muscular) = UPPER(:grupoMuscular)
    """)
    List<ExerciciosEntity> findAllByGrupoMuscularNativeQuery(@Param("grupoMuscular") String grupoMuscular);
}
```

## Documentação JPA Query Methods

https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html