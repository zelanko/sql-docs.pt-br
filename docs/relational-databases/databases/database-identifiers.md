---
title: Identificadores de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1179633f88bef025648b08892859e73b06f14b8
ms.sourcegitcommit: 79d8912941d66abdac4e8402a5a742fa1cb74e6d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80550147"
---
# <a name="database-identifiers"></a>Identificadores de banco de dados

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  O nome do objeto de banco de dados é conhecido como identificador. Tudo no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ter um identificador. Servidores, bancos de dados e objetos de banco de dados, como tabelas, exibições, colunas, índices, gatilhos, procedimentos, restrições e regras, podem ter identificadores. Os identificadores são necessários para a maioria dos objetos, mas são opcionais para alguns objetos, como restrições.

 O identificador de objeto é criado quando o objeto é definido. O identificador é utilizado para referenciar o objeto. Por exemplo, a seguinte instrução cria uma tabela com o identificador `TableX`e duas colunas com os identificadores `KeyCol` e `Description`:

```sql
CREATE TABLE TableX
(KeyCol INT PRIMARY KEY, Description nvarchar(80));
```

 Essa tabela também tem uma restrição sem-nome. A restrição `PRIMARY KEY` não tem identificador.

 A ordenação de um identificador depende do nível em que está definido. Os identificadores de objetos no nível de instância, como logons e nomes de banco de dados, são atribuídos à ordenação padrão da instância. Os identificadores de objetos em um banco de dados, como tabelas, exibições e nomes de coluna, são atribuídos à ordenação padrão do banco de dados. Por exemplo, duas tabelas com nomes que se diferem apenas em maiúsculas e minúsculas podem ser criadas em um banco de dados que possui ordenação que diferencia maiúsculas e minúsculas, mas não podem ser criadas em um banco de dados que tem ordenação que não diferencia maiúsculas e minúsculas.

> [!NOTE]  
> Os nomes de variáveis ou os parâmetros de funções e procedimentos armazenados devem obedecer às regras para identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)] .

## <a name="classes-of-identifiers"></a>Classes de identificadores
Há duas classes de identificadores:

-  Identificadores normais    
   Estão em conformidade com as regras de formato de identificadores. Os identificadores normais não são delimitados quando utilizados em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] .

   ```sql
   USE AdventureWorks
   GO
   SELECT *
   FROM HumanResources.Employee
   WHERE NationalIDNumber = 153479919
   ```

-  Identificadores delimitados    
   Estão entre aspas duplas (") ou colchetes ([]). Os identificadores que estão em conformidade com as regras de formato de identificadores podem não ser delimitados. Por exemplo:

   ```sql
   USE AdventureWorks
   GO
   SELECT *
   FROM [HumanResources].[Employee] --Delimiter is optional.
   WHERE [NationalIDNumber] = 153479919 --Delimiter is optional.
   ```

Os identificadores que não estão em conformidade com todas as regras para identificadores devem ser delimitados em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por exemplo:

```sql
USE AdventureWorks
GO
CREATE TABLE [SalesOrderDetail Table] --Identifier contains a space and uses a reserved keyword.
(
    [Order] [int] NOT NULL,
    [SalesOrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [OrderQty] [smallint] NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NOT NULL,
    [UnitPriceDiscount] [money] NOT NULL,
    [ModifiedDate] [datetime] NOT NULL,
  CONSTRAINT [PK_SalesOrderDetail_Order_SalesOrderDetailID] PRIMARY KEY CLUSTERED 
  ([Order] ASC, [SalesOrderDetailID] ASC)
);
GO

SELECT *
FROM [SalesOrderDetail Table]  --Identifier contains a space and uses a reserved keyword.
WHERE [Order] = 10;            --Identifier is a reserved keyword.
```

Tanto os identificadores normais quanto os delimitados devem conter de 1 a 128 caracteres. Para tabelas temporárias locais, o identificador pode ter no máximo 116 caracteres.

## <a name="rules-for-regular-identifiers"></a>Regras para identificadores normais
 Os nomes de variáveis, funções e procedimentos armazenados devem obedecer às regras de identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)] .

1.  O primeiro caractere deve ser um dos seguintes:

    -   Uma letra, como definido pelo Unicode Standard 3.2. A definição de letras do Unicode inclui caracteres latinos de a até z, de A até Z, além de caracteres de letras de outros idiomas.

    -   Sublinhado (\_), arroba (@) ou tecla jogo da velha (#).

        Determinados símbolos no começo de um identificador possuem um significado especial no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um identificador normal iniciado com arroba denota sempre uma variável local ou parâmetro e não pode ser utilizado como nome de qualquer outro tipo de objeto. Um identificador iniciado com um sinal de número denota uma tabela temporária ou procedimento. Um identificador iniciado com dois sinais de número (##) denota um objeto temporário global. Embora possa ser utilizado um caractere de sinal de número ou dois sinais de número para começar os nomes de outros tipos de objetos, não recomendamos essa prática.

        Algumas funções do [!INCLUDE[tsql](../../includes/tsql-md.md)] têm nomes iniciados com dois sinais de arroba (@@). Para evitar confusão com essas funções, você não deverá usar nomes iniciados por @@.

2.  Os caracteres subsequentes podem incluir:

    -   Letras, como definido no Unicode Standard 3.2.

    -   Números decimais do latim básico ou outros scripts nacionais.

    -   Arroba (@), cifrão ($), sinal de número (#) ou sublinhado.

3.  O identificador não deve ser uma palavra reservada do [!INCLUDE[tsql](../../includes/tsql-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reserva as versões maiúscula e minúscula de palavras reservadas. Quando identificadores são usados nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , os identificadores que não estiverem de acordo com essas regras deverão ser delimitados por aspas duplas ou colchetes. As palavras reservadas dependem do nível de compatibilidade do banco de dados. Esse nível pode ser definido por meio da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) .

4.  Não são permitidos espaços ou caracteres especiais.

5.  Não são permitidos [caracteres suplementares](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters).

 Quando identificadores são usados nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , os identificadores que não estiverem de acordo com essas regras deverão ser delimitados por aspas duplas ou colchetes.

> [!NOTE]
> As regras do formato de identificadores normais dependem do nível de compatibilidade do banco de dados. Esse nível pode ser definido por meio de [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

## <a name="see-also"></a>Consulte Também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
[CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
[CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
[CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
[Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
