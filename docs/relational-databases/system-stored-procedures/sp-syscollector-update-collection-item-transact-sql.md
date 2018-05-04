---
title: sp_syscollector_update_collection_item (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 79232a6bdbc4c56bc52b559a715efb1b9f63e6b9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectorupdatecollectionitem-transact-sql"></a>sp_syscollector_update_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usado para modificar as propriedades de um item de coleta definido pelo usuário ou renomear um desses itens.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_item_id =] *collection_item_id*  
 É o identificador exclusivo que identifica o item de coleta. *collection_item_id* é **int** com um valor padrão de NULL. *collection_item_id* deve ter um valor se *nome* é NULL.  
  
 [ @name =] '*nome*'  
 É o nome do item de coleta. *nome* é **sysname** com um valor padrão de NULL. *nome* deve ter um valor se *collection_item_id* é NULL.  
  
 [ @new_name =] '*novo_nome*'  
 É o novo nome do item da coleta. *Novo_nome* é **sysname**, e se usado, não pode ser uma cadeia de caracteres vazia.  
  
 *Novo_nome* devem ser exclusivos. Para obter uma lista dos nomes dos itens de coleta atuais, consulte a exibição de sistema syscollector_collection_items.  
  
 [ @frequency =] *frequência*  
 É a frequência (em segundos) com que os dados são coletados por esse item de coleta. *frequência* é **int**, com um padrão de 5, o valor mínimo que pode ser especificado.  
  
 [ @parameters =] '*parâmetros*'  
 Os parâmetros de entrada para o item da coleta. *parâmetros* é **xml** com um padrão NULL. O *parâmetros* esquema deve corresponder ao esquema de parâmetros do tipo de coletor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Se o conjunto de coleta estiver definido para o modo não armazenado em cache, a alteração da frequência será ignorada, pois esse modo faz com que a coleção e o carregamento dos dados ocorram conforme a agenda especificada para o conjunto de coleta. Para exibir o status do conjunto de coleta, execute a consulta a seguir. Substitua `<collection_item_id>` pela ID do item de coleta a ser atualizado.  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento, a associação na função de banco de dados fixa dc_admin ou dc_operator (com a permissão EXECUTE) é necessária. Embora dc_operator possa executar esse procedimento armazenado, membros desta função estão limitados nas propriedades que eles podem alterar. As propriedades a seguir só podem ser alteradas através de dc_admin:  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir baseiam-se no item de coleta criado no exemplo definido em [sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md).  
  
### <a name="a-changing-the-collection-frequency"></a>A. Alterando a frequência de coleta  
 O exemplo a seguir altera a frequência de coleta do item de coleta especificado.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. Renomeando um item de coleta  
 O exemplo a seguir renomeia um item de coleta.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. Alterando os parâmetros de um item de coleta  
 O exemplo a seguir altera os parâmetros associados ao item de coleta. A instrução definida no atributo `<Value>` é alterada e o atributo `UseSystemDatabases` é definido como falso. Para exibir os parâmetros atuais deste item, consulte a coluna de parâmetros na exibição de sistema syscollector_collection_items. Talvez seja necessário modificar o valor para `@collection_item_id`.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
