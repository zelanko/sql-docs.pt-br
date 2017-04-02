---
title: "Criando procedimentos armazenados compilados nativamente | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# Criando procedimentos armazenados compilados nativamente
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Os procedimentos armazenados compilados nativamente não implementam a programação [!INCLUDE[tsql](../../includes/tsql-md.md)] completa e a área de superfície da consulta. Há determinadas construções [!INCLUDE[tsql](../../includes/tsql-md.md)] que não podem ser usadas nos procedimentos armazenados compilados nativamente. Para obter mais informações, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 No entanto, existem vários recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)] com suporte apenas nos procedimentos armazenados compilados nativamente:  
  
-   Blocos atômicos. Para obter mais informações, veja [Blocos atômicos](../../relational-databases/in-memory-oltp/blocos-atômicos-nos-procedimentos-nativos.md).  
  
-   Restrições **NOT NULL** nos parâmetros e variáveis dos procedimentos armazenados compilados de modo nativo. Não é possível atribuir valores **NULL** a parâmetros ou variáveis declarados como **NOT NULL**. Para obter mais informações, veja [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"**; -- *(Deve ser inicializado com um valor.)*  
  
    -   SET @myVarchar **= null**; -- *(É compilado, mas falha durante o tempo de execução.)*  
  
-   Associação de esquema de procedimentos armazenados compilados nativamente.  
  
 Procedimentos armazenados compilados de modo nativo são criados com [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). O exemplo a seguir mostra uma tabela com otimização de memória e um procedimento armazenado compilado nativamente usado para inserção de linhas na tabela.  
  
```tsql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 No exemplo de código, **NATIVE_COMPILATION** indica que esse procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] é compilado de modo nativo. As seguintes opções são necessárias:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**SCHEMABINDING**|Um procedimento armazenado compilado nativamente deve ser associado ao esquema dos objetos que ele referencia. Isso significa que as tabelas referenciadas pelo procedimento não podem ser eliminadas. As tabelas referenciadas no procedimento devem incluir o nome do esquema, e não são permitidos curingas (\*) em consultas (ou seja, sem `SELECT * from...`). Há suporte para **SCHEMABINDING** somente nos procedimentos armazenados compilados de modo nativo nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**BEGIN ATOMIC**|O corpo do procedimento armazenado compilado nativamente deve consistir em exatamente um bloco atômico. Os blocos atômicos garantem a execução atômica do procedimento armazenado. Se o procedimento for chamado fora do contexto de uma transação ativa, ele iniciará uma nova transação, que é confirmada no fim do bloco atômico. Os blocos atômicos nos procedimentos armazenados compilados nativamente têm duas opções necessárias:<br /><br /> **TRANSACTION ISOLATION LEVEL**. Veja [Transaction Isolation Levels for Memory-Optimized Tables](../Topic/Transaction%20Isolation%20Levels%20for%20Memory-Optimized%20Tables.md) (Níveis de isolamento da transação para tabelas com otimização de memória) para obter os níveis de isolamento com suporte.<br /><br /> **LANGUAGE**. O idioma do procedimento armazenado deve ser definido para um dos idiomas ou alias de idioma disponíveis.|  
  
## Consulte também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  