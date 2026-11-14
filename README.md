# SQL_BANCO_DE_DADOS_ESCOLA
CREATE DATABASE ESCOLA;
USE ESCOLA;

CREATE TABLE IF NOT EXISTS `aluno` (
	`id_aluno` int AUTO_INCREMENT NOT NULL UNIQUE,
	`nome` varchar(255) NOT NULL,
	PRIMARY KEY (`id_aluno`)
);
CREATE TABLE IF NOT EXISTS `telefone` (
	`id_telefone` int AUTO_INCREMENT NOT NULL UNIQUE,
	`id_aluno` int NOT NULL,
	`telefone` varchar(20) NOT NULL,
	`uq_aluno_telefone` int NOT NULL,
	PRIMARY KEY (`id_telefone`)
);
CREATE TABLE IF NOT EXISTS `matricula` (
	`id_aluno` int NOT NULL UNIQUE,
	`id_turma` int NOT NULL,
	`uq_aluno_turma` int NOT NULL,
	`id_matricula` int NOT NULL,
	PRIMARY KEY (`id_matricula`)
);
CREATE TABLE IF NOT EXISTS `turma` (
	`id_turma` int AUTO_INCREMENT NOT NULL UNIQUE,
	`descricao` varchar(255) NOT NULL,
	PRIMARY KEY (`id_turma`)
);
CREATE TABLE IF NOT EXISTS `oferta_disciplina` (
	`id_oferta` int AUTO_INCREMENT NOT NULL UNIQUE,
	`id_turma` int NOT NULL,
	`id_disciplina` int NOT NULL,
	`id_professor` int NOT NULL,
	`uq_turma_disciplina` int NOT NULL,
	`indice` int NOT NULL,
	PRIMARY KEY (`id_oferta`)
);
CREATE TABLE IF NOT EXISTS `professor` (
	`id_professor` int AUTO_INCREMENT NOT NULL UNIQUE,
	`nome` varchar(255) NOT NULL,
	PRIMARY KEY (`id_professor`)
);
CREATE TABLE IF NOT EXISTS `diciplina` (
	`id_disciplina` int AUTO_INCREMENT NOT NULL UNIQUE,
	`nome` varchar(255) NOT NULL,
	PRIMARY KEY (`id_disciplina`)
);
ALTER TABLE `telefone` ADD CONSTRAINT `telefone_fk1` FOREIGN KEY (`id_aluno`) REFERENCES `matricula`(`id_aluno`);
ALTER TABLE `telefone` ADD CONSTRAINT `telefone_fk2` FOREIGN KEY (`telefone`) REFERENCES `aluno`(`id_aluno`);
ALTER TABLE `turma` ADD CONSTRAINT `turma_fk0` FOREIGN KEY (`id_turma`) REFERENCES `matricula`(`id_turma`);
ALTER TABLE `oferta_disciplina` ADD CONSTRAINT `oferta_disciplina_fk1` FOREIGN KEY (`id_turma`) REFERENCES `turma`(`id_turma`);
ALTER TABLE `oferta_disciplina` ADD CONSTRAINT `oferta_disciplina_fk5` FOREIGN KEY (`indice`) REFERENCES `diciplina`(`id_disciplina`);
ALTER TABLE `professor` ADD CONSTRAINT `professor_fk0` FOREIGN KEY (`id_professor`) REFERENCES `oferta_disciplina`(`id_professor`);
ALTER TABLE `diciplina` ADD CONSTRAINT `diciplina_fk0` FOREIGN KEY (`id_disciplina`) REFERENCES `oferta_disciplina`(`id_disciplina`);
