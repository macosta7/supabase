## Criação das Tabelas

```sql
CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  curso TEXT NOT NULL,
  data_nascimento DATE
);

CREATE TABLE cursos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  alunos_id INT REFERENCES alunos(id) ON DELETE CASCADE,
  cursos_id INT REFERENCES cursos(id) ON DELETE CASCADE,
  data_matricula DATE DEFAULT CURRENT_DATE
);
```

## Inserção de Dados

### Inserção na tabela `alunos`

```sql
INSERT INTO alunos (nome, curso, data_nascimento)
VALUES 
  ('Marcela', 'Engenharia da Computação', '2007-05-30'),
  ('Arthur', 'Adm-Tech', '2005-06-30'),
  ('Adriana', 'Adm-Tech', '2006-11-19'),
  ('Guilherme', 'Ciência da Computação', '2005-02-10'),
  ('Bruno', 'Sistemas de Informação', '2006-12-29'),
  ('Anne', 'Ciência da Computação', '2007-02-21'),
  ('Isaac', 'Engenharia de Software', '2005-09-25'),
  ('Sophia', 'Engenharia da Computação', '2007-03-17'),
  ('Carlos', 'Sistemas de Informação', '2006-05-01'),
  ('Francisco', 'Engenharia da Computação', '2007-06-12');
```

### Inserção na tabela `cursos`

```sql
INSERT INTO cursos (nome, duracao_anos)
VALUES 
  ('Engenharia da Computação', 4),
  ('Engenharia de Software', 4),
  ('Ciência da Computação', 4),
  ('Sistemas de Informação', 4),
  ('Adm-Tech', 4);
```

### Inserção na tabela `matriculas`

```sql
INSERT INTO matriculas (alunos_id, cursos_id)
VALUES 
  (1, 1),
  (2, 5),
  (3, 5),
  (4, 3),
  (5, 4),
  (6, 3),
  (7, 2),
  (8, 1),
  (9, 4),
  (10, 1);
```

## Consulta de Alunos Matriculados

```sql
SELECT a.nome AS aluno, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.alunos_id = a.id
JOIN cursos c ON m.cursos_id = c.id;
```
