# Introdução prática ao Entity Framework 5 Code First (outubro de 2012)

Este documento descreve uma **arquitetura de aplicação ASP.NET flexível e escalável**
e mostra como substituir o ORM **NHibernate** pelo **Entity Framework 5**
sem alterar a camada de aplicação.

🌐 O site associado pode ser acedido em: https://stahe.github.io/pt-ef5cf-oct-2012/

---

## Antecedentes

O **Entity Framework** é um ORM (mapeador relacional de objetos) criado originalmente pela Microsoft
e tornado código aberto em julho de 2012.

Num curso de ASP.NET, este documento baseia-se numa arquitetura em camadas
que permite atualizar tecnologias (ORM, DBMS) sem afetar a aplicação.

---

## Arquitetura geral

O diagrama seguinte mostra as arquiteturas utilizadas na aplicação:
![Arquitetura ASP.NET com NHibernate e Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![Arquitetura ASP.NET com Entity Framework 5 e Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Descrição das camadas

- **Aplicação ASP.NET**  
  Camada de apresentação e lógica de negócio.

- **DAO (Objetos de acesso a dados)**  
  Interface de acesso a dados utilizada pela aplicação.

- **ORM (NHibernate / Entity Framework)**  
  Responsável por gerar SQL e comunicar com o ADO.NET.

- **ADO.NET**  
  Conector ao SGBD.

- **SGBD**  
  Sistema de gestão de bases de dados.

- **Spring.NET**  
  Garantir a integração das camadas e a injeção de dependências.

---

## Porquê utilizar um ORM?

Ligar a camada DAO diretamente ao ADO.NET faz com que a aplicação dependa do SGBD:

- diferenças nos tipos de dados;
- SQL proprietário;
- bibliotecas específicas do SGBD.

Com um ORM, mudar o SGBD equivale essencialmente a **alterar a configuração**
do ORM. A camada DAO permanece inalterada.

---

## Função do Spring.NET

O Spring.NET permite:

- que a aplicação ASP.NET obtenha uma referência à camada DAO;
- a criação desta camada a partir de um ficheiro de configuração;
- a substituição de uma implementação DAO por outra **sem modificar o código**,
  desde que a interface continue a ser a mesma.

---

## Objetivo deste documento

Demonstrar na prática que a arquitetura:

- é **resistente a alterações no SGBD**;
- é **resistente a alterações no ORM**;
- permite **substituir o NHibernate pelo Entity Framework 5**
  sem modificar a camada de aplicação ASP.NET.

---

## Abordagem seguida

A migração é realizada em várias etapas:

1. Exploração do **Entity Framework 5** com vários SGBD;
2. Criação de uma nova camada de acesso aos dados (**DAO2**);
3. Ligação da aplicação ASP.NET existente a esta nova camada DAO.

---

## Destinatários

- Desenvolvedores de ASP.NET
- Estudantes e professores de arquitetura de software
- Qualquer pessoa interessada em arquiteturas desacopladas e escaláveis

---

## Licença e utilização

Documento educativo destinado ao ensino e demonstração
de arquiteturas de aplicações escaláveis.

Serge Tahé, outubro de 2012