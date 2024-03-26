# Exercícios de BD



## 1º Verdadeiro e Falso
|Afirmação|Resposta|
|-|-|
|1|V|
|2|V|
|3|V|
|4|V|
|5|V|

## 2º Verdadeiro e Falso
|Afirmação|Resposta|
|-|-|
|1|V|
|2|V|
|3|V|
|4|V|
|5|F|

## Questão 23
**Alternativa E**

```sql
create database if not exists Ex23;
use Ex23;

create table if not exists Pessoa(
						IdPessoa int not null,
                        Nome varchar(40) not null,
                        Endereco varchar(40),
                        primary key(IdPessoa));
                        
create table if not exists FonePessoa(
						IdPessoa int not null,
                        DDD varchar(3),
                        Prefixo char(4),
                        Nro char(4),
                        foreign key (IdPessoa) references Pessoa(IdPessoa));  

create table if not exists Republica(
						IdRep int not null,
                        Nome varchar(30),
                        Endereco varchar(40),
                        Primary Key(IdRep));   
                        

create table if not exists Estudante(
						RA int not null,
                        email varchar(30),
                        IdPessoa int not null,
                        IdRep int not null,
                        primary key(RA),
						foreign key (IdPessoa) references Pessoa(IdPessoa), 
                        foreign key (IdRep) references Republica(IdRep));  
                        
insert into Pessoa(IdPessoa, Nome, Endereco) values
						(1, "José Silva", "Rua 1, 20");
                        
insert into Republica(IdRep, Nome, Endereco) values
						(20, "Várzea","Rua Chaves, 2001");
```

## 3º Verdadeiro e Falso

|Afirmação|Resposta|
|-|-|
|1|V|
|2|F|
|3|V|
|4|V|
|5|V|

## Questão 40

## A)
```sql
SELECT nome,endereco FROM Cliente WHERE idade < 40
UNION
SELECT nome,endereco FROM Cliente WHERE renda > 30000;
```
## B)
$$
\pi_{\text{nome, endereco}}(\sigma_{\text{idade}\lt40}(\text{Cliente}))
\cup
\pi_{\text{nome, endereco}}(\sigma_{\text{renda}\gt30000}(\text{Cliente}))
$$



## Questão 24
**Alternativa C**

```sql
create database if not exists ex24;

use ex24;


create table if not exists Fornecedor(
							cod_fornec int not null auto_increment,
                            nome_fornec varchar(45),
                            telefone varchar(12),
                            cidade varchar(45),
                            UF varchar(2),
                            primary key(cod_fornec));
                            
create table if not exists Estado(
							UF varchar(2),
                            nome_estado varchar(45));
                            
insert into Fornecedor(nome_fornec, telefone, cidade, UF) values
							("José", "11457886254", "São José dos Campos", "SP"),
                            ("Armando", "21235412563", "Volta Redonda", "RJ"),
                            ("Felipe", "11547895142", "São Paulo", "SP"),
                            ("Mathias", "27124513652", "Vitória", "ES"),
                            ("Rogério", "27852341098", "Vila Velha", "ES");

insert into Estado(UF, nome_estado) values
					("SP", "São Paulo"),
                    ("RJ", "Rio de Janeiro"),
                    ("ES", "Espirito Santo"),
                    ("RS", "Rio Grande do Sul"),
                    ("MG", "Minas Gerais");

select E.nome_estado 
from Estado as E
where E.UF not in (
	select F.UF
    from Fornecedor as F);
```

## Questão 19
**Alternativa E**

```sql
create database if not exists Ex19;
use Ex19;

create table if not exists Partido (
							idPartido int not null,
							siglaPartido varchar(45) not null,
							descricaoPartido varchar(45) not null,
							primary key(idPartido));
 
Create table if not exists Deputado(
							idDeputado int not null,
							idPartido int not null,
							nomeDeputado varchar(45) not null,
							PRIMARY key(idDeputado),
							FOREIGN key(idPartido) REFERENCES Partido(idPartido));

create table if not exists Secao(
							idSecao int not null,
							dataSecao date not null,
							horaSecao time not null,
							decisao varchar(2000) not null,
                            PRIMARY KEY (idSecao));
                            
create table if not exists Participacao(
							idSecao int not null,
							idDeputado int not null,
							FOREIGN key (idSecao) REFERENCES Secao(idSecao),
							foreign key (idDeputado) references Deputado(idDeputado));
                            

insert into Partido(idPartido, siglaPartido, descricaoPartido) values
									(1,"PSDB", "Partido da Social Democracia Brasileira"),
                                    (2,"MBL", "Movimento Brasil Livre");
                                    
insert into Deputado(idDeputado, idPartido, nomeDeputado) values
									(1,1,"Jeremias Carvalho"),
                                    (2,2,"Jadson Mendes"),
									(3,1,"Paulo Júnior"),
                                    (4,2,"Jorge Silva");
                                    
insert into Secao(idSecao, dataSecao, horaSecao, decisao) values
									(1, now(), now(), "Aprovado"),
                                    (2, now(), now(), "Reprovado"),
                                    (3, now(), now(), "Aprovado");

insert into Participacao(idSecao, idDeputado) values
									(1,1),
                                    (2,2),
                                    (3,4);
								
                                
SELECT Deputado.nomeDeputado, Secao.dataSecao FROM Deputado INNER JOIN Participacao 
ON Deputado.idDeputado = Participacao.idDeputado INNER JOIN Secao 
ON Participacao.idSecao=Secao.idSecao;
```

## Questão 30
**"Alternativa C"**

```sql
create database if not exists Ex30;
use Ex30;

create table if not exists Jogador(
				Pseudonimo varchar(10) not null,
                Nome varchar(25) not null,
                Senha varchar(6) not null,
                Primary Key (Pseudonimo));

create table if not exists Nivel(
				Nivel numeric(3) not null,
                NomePseud varchar(10) not null,
                Pontos numeric(5) not null,
                Bonus numeric(5) not null,
                primary key(Nivel, NomePseud),
                foreign key (NomePseud) references Jogador(Pseudonimo));
                
insert into Jogador(Pseudonimo, Nome, Senha) values
				("Vini", "Vinicius", "V123"),
                ("Rod", "Rodrigo", "R123"),
                ("Vic", "Vicente", "VI123"),
                ("Bre", "Breno", "B123"),
                ("Enz", "Enzo", "E123"),
                ("Agat", "Agata", "A123");
                
insert into Nivel (Nivel, NomePseud, Pontos, Bonus) values
				(10, "Vini", 100, 40),
                (11, "Rod", 150, 45),
                (10, "Vic", 125, 60),
                (15, "Bre", 190, 80),
                (6, "Enz", 130, 50),
                (3, "Agat", 50, 20);
  
/*Alternativa C*/             
select Nome, Bonus from Jogador, Nivel where
Jogador.Pseudonimo = nivel.NomePseud order by nivel.Bonus desc;

select Pseudonimo, Bonus from Jogador, Nivel where
Jogador.Pseudonimo = nivel.NomePseud order by nivel.Bonus asc;
```

## Exemplos

```sql
create database if not exists atv03;

use atv03;

-- Funcionarios -----------------------------------------------------------
create table if not exists funcionarios
(
	id_func int auto_increment primary key,
	nome_func varchar(100) not null,
    sexo_func enum("F","M") not null,
    dtadmissao_func date not null,
    salario_func decimal(10,2) not null,
    id_depart int not null,
    foreign key (id_depart) references departamentos (id_depart) 
);

insert into funcionarios (nome_func,sexo_func,dtadmissao_func,salario_func,id_depart) values 
("visconde","M",'1983-02-01',1230.00,3),
("pedrinho","M",'1990-07-29',867.00,3),
("dona benta","F",'1992-11-30',2560.00,1),
("emillia","F",'1998-02-22',1170.00,2),
("rabico","M",'2000-09-08',2300.00,1);


-- Alunos ------------------------------------------------------------------ 
create table if not exists alunos
(
	id_aluno int auto_increment primary key,
    nome_aluno varchar(100) not null,
    sexo_aluno enum("F","M")
);

insert into alunos (nome_aluno,sexo_aluno)   values
("visconde","M"),
("dona benta","F"),
("rabico","M"),
("cuca","F");


-- Departamentos -----------------------------------------------------------
create table if not exists departamentos
(
	id_depart int auto_increment not null primary key,
    nome_depart varchar(30) not null    
);

insert into departamentos (nome_depart)  values
("adminstração"),
("contabilidade"),
("informatica");


-- EXEMPLO 1  - SELEÇÃO 
select * from funcionarios where sexo_func ="F";

-- EXEMPLO 2 - SELEÇÃO 
select * from funcionarios where sexo_func = "M" and salario_func > 1000.00 ; 

-- EXEMPLO 3 - PROJEÇÃO 
select nome_func,sexo_func,salario_func from funcionarios;

-- EXEMPLO 4 - SELEÇÃO E PORJEÇÃO 
select nome_func, salario_func from funcionarios where salario_func>2000.00;

-- EXEMPLO 5 - UNIÃO
select nome_func,sexo_func from funcionarios union
select nome_aluno, sexo_aluno from alunos;

-- EXEMPLO 6 - INSTERSECÇÃO
select nome_func,sexo_func from funcionarios where nome_func in(select nome_aluno from alunos) ;
select nome_func,sexo_func from funcionarios INTERSECT select nome_aluno,sexo_aluno from alunos;
-- ESTA ALEGANDO ERRO, MAS NAO ESTA ERRADO, O WORKBENCH NAO ESTA ACEITANDO O CODIGO, MAS AINDA ASSIM FUNCIONA!!

-- EXEMPLO 7 - DIFERENÇA
select nome_func, sexo_func	 from funcionarios WHERE nome_func NOT IN (select nome_aluno from alunos);
select nome_func, sexo_func	 from funcionarios EXCEPT select nome_aluno,sexo_aluno from alunos;
-- ESTA ALEGANDO ERRO, MAS NAO ESTA ERRADO, O WORKBENCH NAO ESTA ACEITANDO O CODIGO, MAS AINDA ASSIM FUNCIONA!!

-- EXEMPLO 8 - PRODUTO CARTESIANO
select nome_func,sexo_func,dtadmissao_func,nome_depart from funcionarios, departamentos; 

-- EXEMPLO 9 - JUNÇÃO
select funcionarios.nome_func, funcionarios.sexo_func,funcionarios.dtadmissao_func, funcionarios.id_depart, 
		departamentos.id_depart, departamentos.nome_depart from funcionarios inner join departamentos 
        on funcionarios.id_depart = departamentos.id_depart;
        
```