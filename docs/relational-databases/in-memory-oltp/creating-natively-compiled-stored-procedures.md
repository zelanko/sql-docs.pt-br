---
title: Criando procedimentos armazenados compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f81ba5079859508a3806ec33e7d91030e2e787af
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="creating-natively-compiled-stored-procedures"></a>Criando procedimentos armazenados compilados nativamente
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Os procedimentos armazenados compilados nativamente não implementam a programação [!INCLUDE[tsql](../../includes/tsql-md.md)] completa e a área de superfície da consulta. Há determinadas construções [!INCLUDE[tsql](../../includes/tsql-md.md)] que não podem ser usadas nos procedimentos armazenados compilados nativamente. Para obter mais informações, veja [Recursos com suporte para módulos T-SQL compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
No entanto, existem vários recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)] com suporte apenas nos procedimentos armazenados compilados nativamente:  
  
-   Blocos atômicos. Para obter mais informações, veja [Blocos atômicos](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
-   Restrições **NOT NULL** em parâmetros e variáveis. Não é possível atribuir valores **NULL** a parâmetros ou variáveis declarados como **NOT NULL**. Para obter mais informações, consulte [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"**; -- *(Deve ser inicializado com um valor.)*  
  
    -   SET @myVarchar **= null**; -- *(É compilado, mas falha durante o tempo de execução.)*  
  
-   Associação de esquema de procedimentos armazenados compilados nativamente.  
  
Procedimentos armazenados compilados de modo nativo são criados com [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). O exemplo a seguir mostra uma tabela com otimização de memória e um procedimento armazenado compilado nativamente usado para inserção de linhas na tabela.  
  
```sql  
CREATE TABLE [dbo].[T2] (  
  [c1] [int] NOT NULL, 
  [c2] [datetime] NOT NULL,
  [c3] nvarchar(5) NOT NULL, 
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_2] (@c1 int, @c3 nvarchar(5)) 
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
  DECLARE @c2 datetime = GETDATE();  
  INSERT INTO [dbo].[T2] (c1, c2, c3) values (@c1, @c2, @c3);  
END  
GO  
```  
 
No exemplo de código, **NATIVE_COMPILATION** indica que esse procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] é compilado de modo nativo. As seguintes opções são necessárias:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**SCHEMABINDING**|Um procedimento armazenado compilado nativamente deve ser associado ao esquema dos objetos que ele referencia. Isso significa que as tabelas referenciadas pelo procedimento não podem ser eliminadas. As tabelas referenciadas no procedimento devem incluir o nome do esquema, e não são permitidos curingas (\*) em consultas (ou seja, sem `SELECT * from...`). Há suporte para**SCHEMABINDING** somente nos procedimentos armazenados compilados de modo nativo nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**BEGIN ATOMIC**|O corpo do procedimento armazenado compilado nativamente deve consistir em exatamente um bloco atômico. Os blocos atômicos garantem a execução atômica do procedimento armazenado. Se o procedimento for chamado fora do contexto de uma transação ativa, ele iniciará uma nova transação, que é confirmada no fim do bloco atômico. Os blocos atômicos nos procedimentos armazenados compilados nativamente têm duas opções necessárias:<br /><br /> **TRANSACTION ISOLATION LEVEL**. Veja [Transaction Isolation Levels for Memory-Optimized Tables](http://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) (Níveis de isolamento da transação para tabelas com otimização de memória) para obter os níveis de isolamento com suporte.<br /><br /> **LANGUAGE**. O idioma do procedimento armazenado deve ser definido para um dos idiomas ou alias de idioma disponíveis.|  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
