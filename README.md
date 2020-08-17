# exercicio-3
```sql
CREATE TABLE IF NOT EXISTS disciplinas(
	numdisp serial not null,
	nome varchar(90),
	quantcredito int,
	CONSTRAINT disciplinas_pkey PRIMARY KEY (numdisp)
);
```
```sql
CREATE TABLE IF NOT EXISTS cursos(
	numcurso serial not null,
	totalcreditos int,
	nome varchar(90),
	
	CONSTRAINT cursos_pkey PRIMARY KEY (numcurso)

);
```
```sql
CREATE TABLE IF NOT EXISTS professores(
	numprof serial not null,
	nome varchar(90),
	areapesquisa varchar(30),
	
	CONSTRAINT professores_pkey PRIMARY KEY (numprof)
);
```
```sql
CREATE TABLE alunos(
	numaluno serial not null,
	nome varchar(90),
	endereço varchar(255),
	cidade varchar (60),
	telefone varchar (15),
	
	CONSTRAINT alunos_pkey PRIMARY KEY (NUMALUNO)

);
```
```sql
CREATE TABLE IF NOT EXISTS matricula(
	curso int,
	aluno int,
	
	CONSTRAINT matricula_pkey PRIMARY KEY (curso, aluno),
	
	CONSTRAINT curso_fkey FOREIGN KEY (curso) REFERENCES cursos(numcurso),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno)


);
```
```sql
CREATE TABLE aula(
	semestre int,
	nota int,
	aluno int,
	professor int,
	disciplina int REFERENCES disciplinas(numdisp),
	
	CONSTRAINT aula_pkey PRIMARY KEY (semestre,nota),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno),
	CONSTRAINT professor_fkey FOREIGN KEY (professor) REFERENCES professores (numprof)

);
```
```sql
CREATE TABLE contem(
	id SERIAL NOT NULL,
	idcurso int,
	iddisciplinas int,
	
	
	CONSTRAINT contem_pkey PRIMARY KEY (id),
	
	CONSTRAINT curso_fkey FOREIGN KEY (idcurso) REFERENCES cursos(numcurso),
	CONSTRAINT disciplina_fkey FOREIGN KEY (iddisciplinas) REFERENCES disciplinas(numdisp)

);
```
```sql
INSERT INTO cursos(totalcreditos, nome) VALUES (80, 'Ciencia_computacao'), (80, 'Sistemas_informacao'), (70, 'Matematica'); 
INSERT INTO cursos(totalcreditos, nome) VALUES (60, 'História');
```
```sql
INSERT INTO alunos(nome, endereço, cidade, telefone) VALUES ('Marcos João Casanova ', 'Rua da torre', 'Cascais', '9519-6262'), ('Ailton Castro','Rua da Amargura', 'Timbucutu', '9999-6666'), ('Edvaldo Carlos Silva', ' av. Joana Angélica', 'Salvador', '2345-4496'), ('Juvenal', 'av. da abolição', 'Redenção', '4444-2222');
```
```sql
INSERT INTO disciplinas (nome, quantcredito) values('calculo numerico',6),('banco de dados', 4),('Engenharia da computação',4),('teoria geral da administraçao',4),('História Antiga', 4), ('História das artes', 4);
```
```sql
INSERT INTO professores(nome, areapesquisa) VALUES (' Ramon Travanti', 'calculo numerico'), (' Marcos Salvador','teoria geral da administraçao'), ('Juk', ' Banco de Dados'), (' Ramon Travanti', ' Engenharia de Software'), (' Abgair ', 'calculo numerico');
```
```sql
INSERT INTO CONTEM(idcurso, iddisciplinas) VALUES (1,1),(1,2),(1,3),(2,1),(2,2),(2,3),(3,1),(4,5),(4,6);
```
```sql
INSERT INTO matricula (curso, aluno) VALUES (1,1),(2,3),(3,2),(4,4);
```
```sql
INSERT INTO aula( semestre, nota, aluno, professor, disciplina) VALUES (19981, 8, 1, 1, 1), (19981, 5, 2, 1, 1),(19981, 7, 3, 1, 1);
INSERT INTO aula( semestre, nota, aluno, professor, disciplina) VALUES  (19982, 9, 2, 1, 5),(19982, 7, 4, 1, 5);
INSERT INTO aula( semestre, nota, aluno, professor, disciplina) VALUES  (19982, 6, 2, 5, 1),(19982, 10, 4, 5, 1); 
INSERT INTO aula( semestre, nota, aluno, professor, disciplina) VALUES  (19981, 4, 1, 3, 2),(19981, 10, 2, 3, 2),(19981,3,3,3,2);
INSERT INTO aula( semestre, nota, aluno, professor, disciplina) VALUES  (19982, 1, 1, 4, 3),(19982, 8, 2, 4, 3),(19982, 3, 4, 3, 3) ;
```
```sql
--respondido 5
CREATE VIEW RESP05(curso, cod_curso,disciplina)
AS
SELECT DISTINCT C.nome, C.numcurso, D.nome FROM cursos C, disciplinas D, contem T
WHERE C.numcurso = 1 AND T.iddisciplinas = D.numdisp and T.idcurso=1
ORDER BY C.NOME ;
```
```sql
--respondida 6
CREATE VIEW RESP06 (curso,disciplina)
AS
SELECT DISTINCT C.nome, D.nome FROM cursos C, disciplinas D, contem T
WHERE D.numdisp = 1 AND T.iddisciplinas = 1 AND C.numcurso = T.idcurso
ORDER BY C.nome;
```
```sql
--respondida 7
CREATE VIEW RESP07c(nome_aluno, codigo_aluno, semestre, nota, codigo_disciplina, nome_disciplina )
AS
SELECT DISTINCT A.nome, T.aluno, T.semestre, T.nota,T.disciplina, D.NOME FROM alunos A, aula T, disciplinas D
WHERE T.aluno = 1 AND T.semestre = 19981 AND A.numaluno = T.aluno AND T.DISCIPLINA = D.NUMDISP
ORDER BY D.NOME;
```
```sql
--respondida 8
CREATE VIEW RESP08 (nome_aluno, código_aluno, Semestre, nota, disciplina_código, nome_disciplina )
AS
SELECT DISTINCT A.nome, T.aluno, T.semestre, T.nota,T.disciplina, D.NOME FROM alunos A, aula T, disciplinas D
WHERE T.aluno = 2 AND T.nota<7 AND A.numaluno = T.aluno AND T.DISCIPLINA = D.NUMDISP
ORDER BY D.NOME;
```
```sql
--respondida 9
CREATE VIEW RESP09 (nome_aluno, código_aluno, semestre, nota, código_disciplina, nome_disciplina)
AS
SELECT DISTINCT A.nome, T.aluno, T.semestre, T.nota,T.disciplina, D.NOME FROM alunos A, aula T, disciplinas D
WHERE T.disciplina = 1 AND T.nota<7 AND T.semestre = 19981 AND A.numaluno = T.aluno AND T.DISCIPLINA = D.NUMDISP
ORDER BY D.NOME;
```
```sql
--respondida 10
CREATE VIEW RESP10 (nome_professor, semestre, código_disciplia, nome_disciplina)
AS
SELECT DISTINCT P.nome,  T.semestre, T.disciplina, D.NOME FROM professores P, aula T, disciplinas D
WHERE T.professor = 1  AND P.numprof = T.professor AND T.DISCIPLINA = D.NUMDISP AND T.disciplina = 1
ORDER BY D.NOME;
```
```sql
--respondida 11
CREATE VIEW RESP11 (nome_professor, semestre, código_disciplia, nome_disciplina)
AS
SELECT DISTINCT P.nome,  T.semestre, T.disciplina, D.NOME FROM professores P, aula T, disciplinas D
WHERE T.disciplina = 2 AND P.numprof = T.professor AND T.DISCIPLINA = D.NUMDISP
ORDER BY D.NOME;
```
```sql
--respondida12
CREATE VIEW RESP12(NOTA_MINIMA, NOTA_MAXIMA, nota_media)
AS
SELECT  MIN(T.nota), MAX(T.NOTA), AVG(T.nota) FROM aula T, disciplinas D
WHERE T.disciplina = 1 AND D.numdisp = T.disciplina AND T.semestre = 19981;
```
```SQL
-- em resolução 13
SELECT  A.nome AS nome_aluno, T.nota AS NOTAS FROM DISCIPLINAS D,aula T, alunos A
WHERE T.disciplina = 2 AND D.numdisp = T.disciplina AND T.semestre = 19981 AND T.ALUNO = A.numaluno 
GROUP BY A.nome, T.nota;
```
