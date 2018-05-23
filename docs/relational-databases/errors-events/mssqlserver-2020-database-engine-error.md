---
title: MSSQLSERVER_2020 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2020 (Database Engine error)
ms.assetid: 4a8bf90f-a083-4c53-84f0-d23c711c8081
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38f081793e801954229306679d552cea2759df75
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2020"></a>MSSQLSERVER_2020
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2020|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|As dependências reportadas para a entidade "%.*ls" não incluem referências às colunas. Isso ocorre porque a entidade faz referência a um objeto que não existe ou devido a um erro em uma ou mais instruções na entidade.  Antes de executar novamente a consulta, verifique se não há erros na entidade e se todos os objetos referenciados por ela existem.|  
  
## <a name="explanation"></a>Explicação  
A função de sistema **sys.dm_sql_referenced_entities** relatará qualquer dependência em nível de coluna de referências associadas a esquema. Por exemplo, ela reportará todas as dependências em nível de coluna de uma exibição indexada porque uma exibição indexada exige uma associação de esquema. No entanto, quando a entidade referenciada não estiver associada a esquema, as dependências de coluna serão reportadas somente se todas as instruções com referência a essas colunas puderem ser associadas. Será possível associar as instruções com êxito somente se todos os objetos existirem no momento em que as instruções forem analisadas. Se uma instrução definida na entidade não for associada com êxito, as dependências de coluna não serão relatadas e a coluna **referenced_minor_id** retornará 0. Quando não for possível resolver as dependências de coluna, ocorrerá o erro 2020. Esse erro não impede que a consulta retorne dependências no nível do objeto.  
  
## <a name="user-action"></a>Ação do usuário  
Corrija todos os erros identificados na mensagem antes do erro 2020. Por exemplo, no exemplo de código a seguir, a exibição `Production.ApprovedDocuments` é definida nas colunas `Title`, `ChangeNumber` e `Status` da tabela `Production.Document`. A função de sistema **sys.dm_sql_referenced_entities** é consultada para verificar se há colunas e objetos dos quais a exibição `ApprovedDocuments` depende. Como a exibição não foi criada com o uso da cláusula WITH SCHEMA_BINDING, as colunas referenciadas na exibição poderão ser modificadas na tabela da referência. O exemplo altera a coluna `ChangeNumber` da tabela `Production.Document`, renomeando-a para `TrackingNumber`. A exibição `ApprovedDocuments` é consultada novamente na exibição do catálogo; contudo, não é possível associar todas as colunas definidas na exibição. São retornados os erros 207 e 2020 que identificam o problema. Para resolver o problema, a exibição deve ser alterada de modo a refletir o novo nome da coluna.  
  
<pre>USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ApprovedDocuments  
AS  
SELECT Title, ChangeNumber, Status  
FROM Production.Document  
WHERE Status = 2;  
GO  
SELECT referenced_schema_name AS schema_name  
,referenced_entity_name AS table_name  
,referenced_minor_name AS referenced_column  
FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');  
GO  
EXEC sp_rename 'Production.Document.ChangeNumber', 'TrackingNumber', 'COLUMN';  
GO  
SELECT referenced_schema_name AS schema_name  
,referenced_entity_name AS table_name  
,referenced_minor_name AS referenced_column  
FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');  
GO</pre>  
  
A consulta retorna as seguintes mensagens de erro.  
  
<pre>Msg 207, Level 16, State 1, Procedure ApprovedDocuments, Line 3  
Invalid column name 'ChangeNumber'.  
Msg 2020, Level 16, State 1, Line 1  
The dependencies reported for entity  
"Production.ApprovedDocuments" do not include references to  
columns. This is either because the entity references an  
object that does not exist or because of an error in one or  
more statements in the entity. Before rerunning the query,  
ensure that there are no errors in the entity and that all  
objects referenced by the entity exist.</pre>  
  
O exemplo a seguir corrige o nome da coluna na exibição.  
  
<pre>USE AdventureWorks2012;  
GO  
ALTER VIEW Production.ApprovedDocuments  
AS  
SELECT Title,TrackingNumber, Status  
FROM Production.Document  
WHERE Status = 2;  
GO</pre>  
  
## <a name="see-also"></a>Consulte Também  
[sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
