---
description: ALTER SCHEMA (Transact-SQL)
title: ALTER SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c5f444c3866c9660cea1d1396357e276d434a84
ms.sourcegitcommit: 3efd8bbf91f4f78dce3a4ac03348037d8c720e6a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91024411"
---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Transfere um protegível entre esquemas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *schema_name*  
 É o nome de um esquema no banco de dados atual para o qual o protegível será movido. Não pode ser SYS nem INFORMATION_SCHEMA.  
  
 \<entity_type>  
 É a classe da entidade para a qual o proprietário está sendo alterado. Objeto é o padrão.  
  
 *securable_name*  
 É o nome de uma ou duas partes de um protegível no escopo do esquema a ser movido para o esquema.  
  
## <a name="remarks"></a>Comentários  
 Os usuários e esquemas são completamente separados.  
  
 ALTER SCHEMA só pode ser usado para mover protegíveis entre esquemas no mesmo banco de dados. Para alterar ou descartar um protegível dentro de um esquema, use a instrução ALTER ou DROP específica para esse protegível.  
  
 Se o nome de uma parte for usado para *securable_name*, as regras de resolução de nomes atualmente em vigor serão usadas para localizar o protegível.  
  
 Todas as permissões associadas ao protegível serão descartadas quando o protegível for movido para o novo esquema. Se o proprietário do protegível tiver sido definido explicitamente, o proprietário permanecerá inalterado. Se o proprietário do protegível tiver sido definido como SCHEMA OWNER, o proprietário permanecerá como SCHEMA OWNER; entretanto, após a movimentação, SCHEMA OWNER reconhecerá o proprietário do novo esquema. O principal_id do novo proprietário será NULL.  
  
 A movimentação de um procedimento armazenado, uma função, uma exibição ou um gatilho não alterará o nome do esquema, se presente, do objeto correspondente na coluna de definição da exibição do catálogo [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) ou obtido com a função interna [ OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md). Portanto, recomendamos que ALTER SCHEMA não seja usado para mover esses tipos de objeto. Em vez disso, remova e recrie o objeto em seu novo esquema.  
  
 A movimentação de um objeto, como uma tabela ou um sinônimo, não atualizará automaticamente as referências a esse objeto. É necessário modificar manualmente todos os objetos que referenciam o objeto transferido. Por exemplo, se você mover uma tabela e essa tabela for referenciada em um gatilho, será necessário modificar o gatilho para que ele reflita o novo nome do esquema. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para listar as dependências do objeto antes de movê-lo.  

 Para alterar o esquema de uma tabela usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de Objetos, clique com o botão direito do mouse na tabela e, em seguida, clique em **Design**. Pressione **F4** para abrir a janela Propriedades. Na caixa **Esquema**, selecione um novo esquema.  
 
 O ALTER SCHEMA usa um bloqueio no nível do esquema.
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Para transferir um protegível de outro esquema, o usuário atual deve ter permissão CONTROL sobre o protegível (não esquema) e permissão ALTER sobre o esquema de destino.  
  
 Se o protegível tiver uma especificação EXECUTE AS OWNER e o proprietário estiver definido como SCHEMA OWNER, o usuário também deverá ter a permissão IMPERSONATE no proprietário do esquema de destino.  
  
 Todas as permissões associadas ao protegível que estão sendo transferidas serão descartadas após o deslocamento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-transferring-ownership-of-a-table"></a>a. Transferindo a propriedade de uma tabela  
 O exemplo a seguir modifica o esquema `HumanResources` por meio da transferência da tabela `Address` do esquema `Person` para o esquema 'HumanResources'.  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. Transferindo a propriedade de um tipo  
 O exemplo a seguir cria um tipo no esquema `Production` e, em seguida, transfere o tipo para o esquema `Person`.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [VARCHAR](10) NOT NULL ;  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. Transferindo a propriedade de uma tabela  
 O exemplo a seguir cria uma tabela `Region` no esquema `dbo`, cria um esquema `Sales` e, em seguida, move a tabela `Region` do esquema `dbo` para o esquema `Sales`.  
  
```sql  
CREATE TABLE dbo.Region   
    (Region_id INT NOT NULL,  
    Region_Name CHAR(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

