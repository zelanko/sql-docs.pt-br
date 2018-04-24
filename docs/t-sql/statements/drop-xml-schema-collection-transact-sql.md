---
title: DROP XML SCHEMA COLLECTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP XML SCHEMA COLLECTION
- DROP_XML_SCHEMA_COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting XML schema collections
- XML schema collections [SQL Server], removing
- schema collections [SQL Server], removing
- removing XML schema collections
- dropping XML schema collections
- DROP XML SCHEMA COLLECTION statement
ms.assetid: d686f2f5-e03a-4ffe-a566-6036628f46f1
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd78f0f99758a8b570a9d54466c3a46b1133f5d2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="drop-xml-schema-collection-transact-sql"></a>DROP XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui uma coleção de esquema XML inteira e todos os seus componentes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP XML SCHEMA COLLECTION [ relational_schema. ]sql_identifier  
```  
  
## <a name="arguments"></a>Argumentos  
 *relational_schema*  
 Identifica o nome de esquema relacional. Se não for especificado, o esquema relacional padrão será usado.  
  
 *sql_identifier*  
 É o nome da coleção de esquema XML a ser descartada.  
  
## <a name="remarks"></a>Remarks  
 O descarte de uma coleção de esquema XML é uma operação transacional. Isso significa que, ao descartar uma coleção de esquema XML em uma transação e reverter a transação posteriormente, a coleção não será descartada.  
  
 Não é possível descartar uma coleção de esquema XML que está em uso. Desse modo, a coleção que está sendo descartada não pode ser:  
  
-   Associada a nenhum parâmetro ou coluna do tipo **XML**.  
  
-   Especificada em nenhuma restrição de tabela.  
  
-   Mencionada em uma função associada ao esquema ou procedimento armazenado. Por exemplo, a função a seguir bloqueará a coleção de esquema XML `MyCollection` porque a função especifica `WITH SCHEMABINDING`. Se essa especificação for removida, não haverá nenhum bloqueio em XML SCHEMA COLLECTION.  
  
    ```  
    CREATE FUNCTION dbo.MyFunction()  
    RETURNS int  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
       ...  
       DECLARE @x XML(MyCollection)  
       ...  
    END;  
    ```  
  
## <a name="permissions"></a>Permissões  
 O descarte de XML SCHEMA COLLECTION requer uma permissão DROP na coleção.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a remoção de uma coleção de esquema XML.  
  
```  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)   
 [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
