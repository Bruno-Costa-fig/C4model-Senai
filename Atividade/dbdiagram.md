Table aluno {
  id int [pk, increment]
  nome varchar(100) [not null]
  matricula varchar(20) [unique, not null]
  created_at timestamp [default: `now()`]
}

Table turma {
  id int [pk, increment]
  nome varchar(50) [not null, note: 'Ex: DS-2024-1']
  periodo varchar(20) [not null, note: 'Ex: Matutino']
  created_at timestamp [default: `now()`]
}

Table aluno_turma {
  aluno_id int [not null]
  turma_id int [not null]

  indexes {
    (aluno_id, turma_id) [pk]
  }
}

Table aula {
  id int [pk, increment]
  turma_id int [not null]
  data date [not null]
  descricao varchar(200)
}

Table presenca {
  id int [pk, increment]
  aula_id int [not null]
  aluno_id int [not null]
  presente boolean [not null, default: false]
  registrado_em timestamp [default: `now()`]
}

Ref: aluno_turma.aluno_id > aluno.id
Ref: aluno_turma.turma_id > turma.id
Ref: aula.turma_id > turma.id
Ref: presenca.aula_id > aula.id
Ref: presenca.aluno_id > aluno.id