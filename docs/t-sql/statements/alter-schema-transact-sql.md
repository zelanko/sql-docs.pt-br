---
title: ALTER SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad157c7d4d7b92bc199c4a490d4387acc0af0908
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Transfere um protegível entre esquemas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome de um esquema no banco de dados atual para o qual o protegível será movido. Não pode ser SYS nem INFORMATION_SCHEMA.  
  
 \<entity_type >  
 É a classe da entidade para a qual o proprietário está sendo alterado. Objeto é o padrão.  
  
 *securable_name*  
 É o nome de uma parte ou de duas partes de um protegível contido em esquema a ser movido para o esquema.  
  
## <a name="remarks"></a>Comentários  
 Os usuários e esquemas são completamente separados.  
  
 ALTER SCHEMA só pode ser usado para mover protegíveis entre esquemas no mesmo banco de dados. Para alterar ou descartar um protegível dentro de um esquema, use a instrução ALTER ou DROP específica para esse protegível.  
  
 Se um nome de uma parte é usado para *securable_name*, as regras de resolução de nome atualmente em vigor serão usadas para localizar o protegível.  
  
 Todas as permissões associadas ao protegível serão descartadas quando o protegível for movido para o novo esquema. Se o proprietário do protegível tiver sido definido explicitamente, o proprietário permanecerá inalterado. Se o proprietário do protegível tiver sido definido como SCHEMA OWNER, o proprietário permanecerá como SCHEMA OWNER; entretanto, após a movimentação, SCHEMA OWNER reconhecerá o proprietário do novo esquema. O principal_id do novo proprietário será NULL.  
  
 Para alterar o esquema de uma tabela ou exibição usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de objetos, clique com botão direito da tabela ou exibição e, em seguida, clique em **Design**. Pressione **F4** para abrir a janela Propriedades. No **esquema** , selecione um novo esquema.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Para transferir um protegível de outro esquema, o usuário atual deve ter permissão CONTROL sobre o protegível (não esquema) e permissão ALTER sobre o esquema de destino.  
  
 Se o protegível tiver uma especificação EXECUTE AS OWNER e o proprietário estiver definido como SCHEMA OWNER, o usuário deverá ter também permissão IMPERSONATION sobre o proprietário do esquema de destino.  
  
 Todas as permissões associadas ao protegível que estão sendo transferidas serão descartadas após o deslocamento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-transferring-ownership-of-a-table"></a>A. Transferindo a propriedade de uma tabela  
 O exemplo a seguir modifica o esquema `HumanResources` por meio da transferência da tabela `Address` do esquema `Person` para o esquema.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. Transferindo a propriedade de um tipo  
 O exemplo a seguir cria um tipo no esquema `Production` e, em seguida, transfere o tipo para o esquema `Person`.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [varchar](10) NOT NULL ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
  
-- Change the type to the Person schema.  
ALTER SCHEMA Person TRANSFER type::Production.TestType ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. Transferindo a propriedade de uma tabela  
 O exemplo a seguir cria uma tabela `Region` no `dbo` esquema, cria um `Sales` esquema e, em seguida, move o `Region` tabela o `dbo` esquema para o `Sales` esquema.  
  
```  
CREATE TABLE dbo.Region   
    (Region_id int NOT NULL,  
    Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar esquema &#40; Transact-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


