# Views-SQL

# Exercício - Views (SQL)

Este documento contém a resolução dos exercícios sobre criação de **views** (visões) em SQL, conforme solicitado no material de estudo.

As views são tabelas virtuais baseadas em consultas `SELECT`, utilizadas para simplificar consultas complexas, restringir acesso a dados e promover independência de dados.

---

## a) Visão dos CDs gravados pela gravadora 2

```sql
CREATE VIEW v_cd_gravadora2 AS
SELECT *
FROM cd
WHERE grav_id = 2;
```

---

## b) Visão dos CDs e suas respectivas gravadoras

```sql
CREATE VIEW v_cd_gravadora AS
SELECT cd.cd_nome, gravadora.grav_nome
FROM cd
JOIN gravadora ON cd.grav_id = gravadora.grav_id;
```

---

## c) Visão das músicas e seus respectivos autores

```sql
CREATE VIEW v_musica_autor AS
SELECT musica.mus_nome, autor.autor_nome
FROM musica
JOIN autor ON musica.autor_id = autor.autor_id;
```

---

## d) Visão das músicas, sua duração e o CD a que pertencem

```sql
CREATE VIEW v_musica_cd AS
SELECT musica.mus_nome, musica.mus_duracao, cd.cd_nome
FROM musica
JOIN item_cd ON musica.mus_id = item_cd.mus_id
JOIN cd ON item_cd.cd_id = cd.cd_id;
```

---

## e) Visão dos autores e as gravadoras onde possuem CDs gravados

```sql
CREATE VIEW v_autor_gravadora AS
SELECT autor.autor_nome, gravadora.grav_nome
FROM autor
JOIN musica ON autor.autor_id = musica.autor_id
JOIN item_cd ON musica.mus_id = item_cd.mus_id
JOIN cd ON item_cd.cd_id = cd.cd_id
JOIN gravadora ON cd.grav_id = gravadora.grav_id
GROUP BY autor.autor_nome, gravadora.grav_nome;
```

---

## Observações

- As views criadas seguem a classificação apresentada no material:
  - **Simples**: quando utilizam apenas uma tabela (exemplo **a**).
  - **Complexas**: quando utilizam junções (`JOIN`), funções ou agrupamentos (exemplos **b**, **c**, **d**, **e**).
- O comando `DROP VIEW` pode ser utilizado para excluir uma view, caso necessário:
  ```sql
  DROP VIEW v_cd_gravadora2;
  ```

---
