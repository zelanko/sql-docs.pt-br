---
title: IDENTITY (função) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ecb2be9e90d1085f9c0badb84174a6688a91903d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="identity-function-transact-sql"></a>IDENTITY (função) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  É usada somente em uma instrução SELECT com uma cláusula INTO *table* para inserir uma coluna de identidade em uma nova tabela. Embora similar, a função IDENTITY não é a propriedade IDENTITY que é usada com CREATE TABLE e ALTER TABLE.  
  
> [!NOTE]  
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_type*  
 É o tipo de dados da coluna de identidade. Os tipos de dados válidos para uma coluna de identidade são tipos de dados da categoria de tipo de dados inteiro, exceto para os tipos de dados **bit** ou **decimal**.  
  
 *seed*  
 É o valor inteiro que será atribuído à primeira linha da tabela. A cada linha seguinte é atribuído o próximo valor de identidade, que é igual ao ultimo valor IDENTITY mais o valor de *increment*. Se *seed* nem *increment* for especificado, ambos usarão 1 como padrão.  
  
 *increment*  
 É o valor inteiro a ser adicionado ao valor *seed* para linhas sucessivas na tabela.  
  
 *column_name*  
 É o nome da coluna que será inserida na nova tabela.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo que *data_type*.  
  
## <a name="remarks"></a>Remarks  
 Como essa função cria uma coluna em uma tabela, um nome para a coluna deve ser especificado na lista de seleção de uma destas maneiras:  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir insere todas as linhas da tabela `Contact` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]em uma nova tabela chamada `NewContact`. A função IDENTITY é usada para iniciar números de identificação em 100, em vez de 1, na tabela `NewContact`.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SELECT @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
