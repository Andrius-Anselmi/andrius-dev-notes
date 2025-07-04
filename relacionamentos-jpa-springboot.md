
# 📘 Conceitos Fundamentais de Relacionamentos com JPA no Spring Boot

## 🔹 1. Entidade (Entity)
- Representa uma tabela no banco de dados.
- É uma classe Java anotada com `@Entity`.
- Possui um identificador único (`@Id`), geralmente `Long` ou `UUID`.

```java
@Entity
public class Produto {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nome;
}
```

---

## 🔹 2. Chave Primária (Primary Key)
- Identificador único do registro.
- Declarada com `@Id`.
- Pode ser autogerada com `@GeneratedValue`.

---

## 🔹 3. Chave Estrangeira (Foreign Key)
- Liga duas tabelas no banco.
- Criada com `@ManyToOne`, `@JoinColumn`, etc.

---

## 🔹 4. Tipos de Relacionamento

### ➤ @ManyToOne (muitos para um)
- Fica no lado que contém a FK.
- Exemplo: vários alunos pertencem a uma turma.

```java
@ManyToOne
@JoinColumn(name = "turma_id")
private Turma turma;
```

---

### ➤ @OneToMany (um para muitos)
- Usado com `mappedBy`.
- Representa uma lista de objetos relacionados.

```java
@OneToMany(mappedBy = "turma", cascade = CascadeType.ALL)
private List<Aluno> alunos;
```

---

### ➤ @OneToOne
- Um registro para outro único registro.
- Ex: usuário e perfil.

---

### ➤ @ManyToMany
- Requer tabela de junção com `@JoinTable`.
- Exemplo: alunos e cursos.

```java
@ManyToMany
@JoinTable(
    name = "aluno_curso",
    joinColumns = @JoinColumn(name = "aluno_id"),
    inverseJoinColumns = @JoinColumn(name = "curso_id")
)
private List<Curso> cursos;
```

---

## 🔹 5. mappedBy
- Define o lado **não dono** do relacionamento.
- Evita criação automática de tabela de junção desnecessária.

---

## 🔹 6. @JoinColumn
- Define a coluna FK no banco.
- Usado em `@ManyToOne`, `@OneToOne`, etc.

---

## 🔹 7. Evitar loops no retorno JSON
- Use `@JsonIgnore`, `@JsonManagedReference`, ou `@JsonBackReference`.

```java
// Lado ignorado na serialização
@JsonBackReference
@ManyToOne
private Turma turma;

@JsonManagedReference
@OneToMany(mappedBy = "turma")
private List<Aluno> alunos;
```

---

## 🔹 8. Conceitos de Banco que você precisa entender

- Entidades e relacionamentos
- Diferença entre PK e FK
- Modelagem de dados (DER)
- Relacionamentos: 1:1, 1:N, N:N
- Tabelas de junção
- Normalização: 1FN, 2FN, 3FN

---

## 🔹 9. Melhores práticas

- Pense quem possui a FK (quem é o "lado dono")
- Use `@JoinColumn` para controle explícito
- Evite loops em JSON
- Separe entidades de DTOs
- Entenda os conceitos, não decore tudo

---

## 🔹 10. Não precisa decorar tudo
- Consultar a sintaxe é normal.
- O importante é entender o que está fazendo.
- Use documentação e exemplos como ferramenta.

---
