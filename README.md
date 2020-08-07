# exercicio-3

CREATE TABLE IF NOT EXISTS disciplinas(
	numdisp serial not null,
	nome varchar(90),
	areapesquisa varchar(30),
	CONSTRAINT disciplinas_pkey PRIMARY KEY (numdisp)
);

CREATE TABLE IF NOT EXISTS cursos(
	numcurso serial not null,
	totalcreditos int,
	nome varchar(90),
	
	CONSTRAINT cursos_pkey PRIMARY KEY (numcurso)

);

CREATE TABLE IF NOT EXISTS professores(
	numprof serial not null,
	nome varchar(90),
	areapesquisa varchar(30),
	
	CONSTRAINT professores_pkey PRIMARY KEY (numprof)
);

CREATE TABLE alunos(
	numaluno serial not null,
	nome varchar(90),
	endereço varchar(255),
	cidade varchar (60),
	telefone varchar (15),
	
	CONSTRAINT alunos_pkey PRIMARY KEY (NUMALUNO)

);

CREATE TABLE IF NOT EXISTS matricula(
	curso int,
	aluno int,
	
	CONSTRAINT matricula_pkey PRIMARY KEY (curso, aluno),
	
	CONSTRAINT curso_fkey FOREIGN KEY (curso) REFERENCES cursos(numcurso),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno)


);

CREATE TABLE aula(
	semestre int,
	nota int,
	aluno int,
	professor int,
	
	CONSTRAINT aula_pkey PRIMARY KEY (semestre,nota),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno),
	CONSTRAINT professor_fkey FOREIGN KEY (professor) REFERENCES professores (numprof)

);

CREATE TABLE aula(
	semestre int,
	nota int,
	aluno int,
	professor int,
	
	CONSTRAINT aula_pkey PRIMARY KEY (semestre,nota),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno),
	CONSTRAINT professor_fkey FOREIGN KEY (professor) REFERENCES professores (numprof)

);
